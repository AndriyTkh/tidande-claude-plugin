# Investigations, claims and proposals

## An investigation

Your own working folder in Tidande: notes, leads, claims, post sets, links, files. Claude can work
only in investigations it is allowed into: your own, at the public level, with "доступ з асистента"
switched on in the investigation's popover in the web app. An investigation Claude creates for you
(`investigation_create`) starts with it on. Your private investigations stay closed to Claude.

## A proposal

Everything Claude writes is a proposal. It is marked as written by the assistant and shows which
client wrote it. You review it in the Tidande web app, where you confirm, edit or discard it. Claude
never calls a claim confirmed, true or proven; only you confirm.

## A claim and a verified quote

A claim is one checkable fact: neutral, dated, with the speaker and how they said it (stated,
reported, plans, alleged, rumour, record). Its evidence is a fragment of a stored post, written as
`<post id>#<start>-<end>`. Code, not Claude, cuts the fragment from the stored text and checks it
(`claim_propose`, `quotes_resolve`). A quote that does not match is refused; the fix is to read the
post again, never to retype the quote.

- A preview in a search result is not a quote.
- Claude's own reading (motive, ranking, "this suggests") is saved as an interpretation, not a claim.
- A newer claim can replace an older one (`claim_supersede`); the old one stays in the history.

## Reviewing in the web app

Open Tidande, choose the investigation, and read: claims with their quotes and links to the posts,
notes, leads, the timeline and the graph. Ask Claude "що ти запропонував записати і де це
подивитись" to get the list.

## Memory

Before repeating work Claude looks at what the investigation already holds (`ws_view`, `recall`,
`ws_search`). A new chat can continue an old investigation: name it.
