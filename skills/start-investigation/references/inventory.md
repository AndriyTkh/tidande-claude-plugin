# Case Inventory and triage

## The Case Inventory (what this case already did)

The server records, by code, every post and registry record a reader returned. Agents write only
verdicts. The state lives in the investigation's own log, so it survives between calls and between
sessions. In order:

1. **Direction.** The Navigator gives the direction id (`D1`, `D2`, ...). At the start of a line call
   `direction_set` with `action: open` and that id (no title: free text stays out of the log). When
   the line stops, `park` or `close` it. The next `open` returns the start of that direction's
   re-look queue (items skipped or deferred elsewhere, ordered by links to the posts you kept).
2. **Parallel lines.** With one direction open, a call belongs to it. With several open, pass
   `direction` on every `item_verdict`, `search` and `post_set_members`: `item_verdict` without it
   is refused (the message lists the open ids); a search or set listing without it hides nothing.
3. **After each reader slice** call `item_verdict` once for the whole slice: `in` for what you keep,
   `out` with a reason code (`off_topic`, `pr_only`, `background`, `duplicate_of:<id>`,
   `no_new_fact`, `outside_window`, `unreadable`) for what you skip, `deferred` for a maybe. An `in`
   takes a fact type (`money_figure`, `court_step`, `appointment`, `contract`, `ownership`,
   `statement`, `date_event`, `other`); a `dropped_unread` takes a filter code (`triage`,
   `rank_threshold:0.3`); only `deferred` takes a short note. A note or `by` that holds a personal
   name, an e-mail or a long number is refused; `by` is a role or line slug (`reader-1`).
4. **Read the replies.** `inventory.hidden_here` counts hits this direction already judged (ids in
   `hidden_ids`; `item_verdict` with `pending` brings one back). `known` lists posts judged in
   another direction: read them again only if this direction's question differs. `deferred` and
   `stale` hits are marked. `get_posts` returns the text as always, with `inventory.known` per
   post. A reply with `events_dropped` or `write_failures` says the log is not keeping up.
5. **At every loop boundary** call `inventory_status` and act on the open lists: `kept_not_claimed`
   (claim it or give it an `out` reason), `read_not_judged` (judge it), `records_touched_not_stated`
   (state it in a claim or record, or judge it `out`), and the `relook` queue (take the top of it).

A verdict is about one direction, not about the post: a post skipped for one line can be exactly
what another line needs.

## Triage of a big candidate set (`triage_posts`, when listed)

A captain's candidate set is often several hundred posts. `triage_posts` has a small, cheap model
read every candidate on the server and keep the best share, so the readers read only that share.
It runs on Tidande's own account: a call is capped (`max_cost_usd`, never above one dollar) and
counts toward a daily limit; if the limit is reached the call answers `fallback: true`.

1. Call it with `question` (the topic-level question of the direction, not a narrow per-line one),
   `topic` (one short paragraph: topics and entities only; no answers, numbers or post ids) and
   `post_set` (the candidate set). `keep_rule` is `score` by default on this service: it keeps every
   post scored 2 or 3, best first, at most half of the candidates, and retries unscored posts once.
   Leave `keep_share` alone with `score`.
2. The reply gives `kept_set` (ranked) and `dropped_set` (nothing is lost): name them in the thread
   note. Cut reader slices of 40-50 from `kept_set` in its order. `fallback: true` means the model
   failed or a cap was reached: the kept set is only the first posts of the input order; say so in
   the thread note and decide whether to read more of the candidates. `unanswered` posts rank last.
3. Give `audit_ids` (a random sample of the dropped posts) to ONE reader, with the usual reader
   brief and no hint that they were dropped. The audit miss rate is the audit ids the reader put in
   `in`, over those it judged. Record it as an item of the thread note with the tag `triage-audit`.
   When it is above 0.2, read the dropped set's best-ranked posts (`post_set_members` on
   `dropped_set`) with at least one more reader slice before the thread stops.
4. `fragment_hints` are character spans of the stored text where the model would look: pointers,
   never quotes. A reader opens the post, reads it and cites a fragment id from `get_post` after
   `quotes_resolve`.

Without `triage_posts` (not listed, or refused), rank the candidates with `post_set_members`
(`rank_by`, up to 3 scope queries) and read slices from the top.

## Scale

A search page is up to 100 hits; `cursor` pages a ranked list; post sets up to 5,000 posts; set
listings 200 a page. Cut the period into month windows and run the same queries in each. Put each
window or angle in a `post_set`, rank it before reading, keep one "read so far" set (`post_set` with
`document_ids` and `extend`, appended by one agent one call at a time) and pass it as
`exclude_post_sets` in every later wave. Give readers ids, never text, and resolve what they return
with `quotes_resolve`.
