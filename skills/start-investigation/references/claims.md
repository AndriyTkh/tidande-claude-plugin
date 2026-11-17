# Claims, promotion and the final write-up

## Claims and quotes (rules that cannot be bent)

- A quote is a fragment id (`<document id>#<start>-<end>`) taken from `get_post`. Never type a
  quote. `claim_propose` takes the quote from the stored text and verifies it in code; any failing
  fragment refuses the claim. Fix the statement or the span, never the evidence.
- One checkable fact per claim, neutral, complete, dated (`event_date`; `valid_from` and `valid_to`
  for a state over a period). Supporting claims go in `deps`.
- Your reading (motive, ranking, "this suggests") is an `interpretation` item (`ws_append_item`),
  shown as a proposal, never as a fact.
- Edited or deleted posts are findings: cite the version you read.
- A claim carries its own status. Do not call one confirmed unless the tool result says so.
- Never profile a private person.

## Statements (what `claim_propose` reads)

English, one fact, neutral, with the figure as digits and the speaker's qualifier as a tag at the
END: `... stated that 987 mln UAH went to protection (stated).` The tag is one or more of `stated`,
`reported`, `plans`, `alleged`, `rumour`, `record` in one pair of brackets. Meanings: `stated` (the
speaker's own statement), `reported` (an outlet reports what someone else said or did), `plans` (an
intent, not a fact done), `alleged` (suspicion, accusation), `rumour` (anonymous sources), `record`
(a document or registry row). A keep has ONE qualifier.

Figures: UAH, USD and EUR with `thousand`, `mln`, `million`, `bn`, `billion`; digits with comma or
space thousands; decimals with a point or comma; counts with nouns; hedges (`over`, `almost`,
`about`, `at least`, `up to`); tonnes, hours, days; dates. Words for numbers are not read: write
digits. A `number` claim takes `quantity` (`value`, `unit` = the counted noun, `qual`, `subject`)
when the figure is a bare count; one figure per claim. A statement with two figures is split. A
`period` must be the date the statement states.

## Every keep and record ends somewhere

Every post a reader kept ends as a claim or a written skip with a real reason. Every registry
record a line opens ends as a statement (amount, date, party) or "checked, nothing relevant". The
Case Inventory's `inventory_status` lists what is still open; do not hand over while it is not empty
without saying so.

## Attribution check before promotion

A wrong speaker or a dropped qualifier is the common error. Before promoting, re-read each claim's
fragment (`quotes_resolve`, at most 10 posts at a time), write your own reading of who says what and
how, and compare it with the claim's tag. A disagreement means the statement may be wrong:
`claim_supersede` it and name the old id. A `ws_*` call takes the bare claim id, without the `clm-`
prefix shown in a record header.

## Promotion

Only the lead promotes. A note titled `Promoted from T<n>`, header `tags: [promoted, "thread:T<n>"]`
and `claims: [<ids>]`, one item per claim with a reason. No quota and no percentage: promote every
distinct, dated, attributed claim that supports a conclusion or answers a sub-question, with its
chain of evidence; leave out background, PR lines and claims that led to no conclusion. Several
hundred promoted claims is too many for a human to check. Routes that led nowhere are not claims;
each gets one short `dead_ends` line (route, what was checked, why it ended). A captain never
promotes its own claim. Write or patch the promotion notes only after the check, so no superseded id
stays in them.

## Verify and write the final answer

1. A fresh sub-agent reads every claim statement against its quote or record and fixes any statement
   that says more than its quote.
2. Check that every string in quotation marks in the final text sits inside the verified quote of a
   claim cited on the same line. A paraphrase of reported speech, a translation or a label does not.
   Quote the stored words, or drop the quotation marks.
3. The final text goes per direction: terms and their status, the claims behind each, what was not
   found and what was tried, open leads, and a short "Explored, led nowhere" section. Every statement
   cites claim ids (with the chain of evidence) or is labelled interpretation. Report the share of
   claims from the subject's own channels apart.
4. Cite by claim id and fragment id plus the post url from `get_post`; say what each registry row is
   (source, record id, snapshot date). State coverage plainly: the period searched, channels that
   were silent, what was not found and which queries were tried. Web results are leads, not evidence.
5. Keep it in the investigation (a note) and tell the person where to review it in the Tidande web
   app. The journalist confirms. Never call a claim confirmed, true, proven or false.

## When something fails

- `claim_unverified` or `claim_no_evidence`: the fragment does not support the words; read the post
  again.
- `rate_limited`: slow down. `run_in_progress`: the in-app agent is working there; wait a minute and
  retry once.
- A tool says it is not available (for example triage): carry on without it and say so.
- A final message from a sub-agent that is not its own result means it did not finish: check what it
  wrote in the investigation before starting another.
