# Roles and briefs

The investigation is the system of record; a summary is a lead, and nobody below the lead is replaced
by a summary of itself. The sub-agents ship with the plugin: `tidande:captain`, `tidande:reader`,
`tidande:claimer` (model Sonnet; you stay on the person's own model). They use Tidande tools only.

| role | holds | writes | context |
|---|---|---|---|
| lead (you) | study map, one report per thread, promotions | the study map note, interpretations, promotions, the final report | work through a long run; keep the study map note current, it is what survives a compaction |
| captain | one direction's candidate set, slices, thread note | post sets, thread note, leads, links | at most 100 k; at 100 k update the thread note and stop, you start a fresh captain from the note |
| reader | one slice of 40-50 post ids, or one registry route | verdicts (`item_verdict`) only | at most 60 k |
| claimer | at most 25 reader keeps | claims through `claim_propose` | at most 60 k |

At most 5 captains at once, at most 4 readers at once, at most 3 claimers writing at once (the claim
write limit bites at 5). All foreground. Only claimers and captains write facts, only through
`claim_propose` (code verifies quotes and dedupes). Interpretations, promotions and the report are
yours.

## Brief to a captain (fill the brackets, keep it short)

Direction and its terms; the investigation id; scope (channels, window, registries); the other
lines' latest read-set ids to pass as `exclude_post_sets`; a budget (steps, slices); the stop rule
(two reader slices in a row with no new claim on a term). Say: "Return a slice plan; do not claim."

## What a captain returns

One JSON object, ids and counts only, at most 1.5 k tokens: `thread`, `direction`, `summary` (three
sentences), `sets` (candidates, kept, dropped: id and count), `slices` (a list of post-id lists of
40-50), `triage` (counts, audit ids, `fallback`), `leads`, `dead_ends`, `coverage` (windows,
channels, silent). No quote or post text anywhere. Save it as the first item of the thread note
(tag `thread:T<n>`, status `live`, or `parked` when it ends; `done` is not a status).

## Reader (one slice)

Reads with `get_posts` (batches of up to 50) and judges each post against each sub-question of the
line: in scope if it holds one checkable fact for any of them, even when the post is mostly about
something else. Fact types: a money figure (budget, price, contract value, payment); a date or a
court step (suspicion, measure of restraint, charge, hearing, verdict, appeal); an appointment or
dismissal; a contract or tender (id, buyer, winner, value, change); a statement by an official (who,
when, what was promised or denied). One keep is one fact (one fragment); a post with three facts has
three keeps. After the slice the reader calls `item_verdict` once for the whole slice, passing the
direction id: `in` (with a fact type), `out` (with a reason code), `deferred`. It returns JSON
(at most 600 tokens): `in`, `out`, `keep` (each `{post, fragment_ids, sub_q, fact_type, why}`),
`leads`, `errors`. Never quote text; never `claim_propose`; stop after 3 tool errors.

## Claimer (one batch of keeps)

1. Page the whole claim index (`ws_view` on `/files/claim/INDEX.md`, every page, to the end) and
   build a table of post, figure, date and speaker; re-page after every 20 claims written (others
   write at the same time). A sample is not a check.
2. `quotes_resolve` all fragment ids of the batch (up to 200 a call). Never type a quote.
3. For each keep: a duplicate of an existing claim (same speaker, figure and date) is skipped with
   the claim id; otherwise one `claim_propose`: one fact, statement as in the claims reference,
   `fragment_ids`, `event_date`, `claim_type`.
4. Every keep ends as a claim, or a duplicate, `off_question`, `opinion` or `other` with a real note
   of at most 20 words (not "not claimed"). A refused claim: fix the statement once; if it still
   fails, `other` with "claim refused: why".
5. Return counts and ids only (at most 600 tokens). Never message a finished claimer, reader or
   captain (it restarts and files again); leftovers go to a new claimer whose batch excludes every
   post already handled.

## Registry-only lines

A line that reads only registries has no readers: the captain opens records and each one ends as a
statement (amount, date, party) in a claim or record (`money_record_add`, `timeline_event_add`) or as
"checked, nothing relevant" with a note.
