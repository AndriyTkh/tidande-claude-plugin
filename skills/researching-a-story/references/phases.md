# The research phases in detail

## Gather

- 8 to 15 varied `search` queries: the topic's own words, Ukrainian and Russian spellings,
  transliterations, nicknames, company and event names, the likely headline wording. Mode `hybrid`
  first, `bm25` for exact names, `dense` for paraphrase.
- Run each with and without a date window, and per channel group with `channels`;
  `exclude_channels` drops sources already covered. Page deep lists with `cursor`.
- Volume questions (how many, how it spread): a `post_set`, then `aggregate` and `post_timeline`;
  the posts stay on the server. `post_set_members` lists a set a page at a time (previews route
  your reading; a preview is never a quote).
- Keep a note (`ws_create`, type note): the queries run, what each found, what is missing.

## Compare sources

- Find the earliest post that carries the fact (a narrow window; read `published_at`).
- `event_of` on hit ids shows the stored event card and its channels; `event_view` opens it.
- Several channels repeating one origin are one source. Where sources disagree, keep both as claims
  and link them with `ws_link` kind `contradicts`; state the difference as dated facts.
- An official body's own channel and the state registries are primary for their own acts.

## Chronology

- `timeline` on the topic with the window; widen it if the first card is at its edge.
- `post_set` plus `post_timeline` (day, week or month) for first and last seen, peaks and gaps.
- For each turning point: `event_view`, `get_post`, a dated claim (`event_date`).
- Look for sequences: statement then denial, tender then contract then change, claim then
  correction. Link steps with `ws_link` kind `follows_up`.

## Gaps

- For each question: answered (claim ids), partly, or not found (with the queries and windows tried).
- The corpus covers a limited period; say so when a question reaches outside it.
- Write a `lead` (`ws_create`, type lead) for each open question, so the next session starts there.

## Report

- A note whose items each cite claim ids; your reading as `interpretation` items (`ws_append_item`).
- In the chat answer cite by claim id and fragment id (`<document_id>#<start>-<end>`) plus the post url.
