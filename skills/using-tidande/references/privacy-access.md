# Privacy, access and the research level

## What Claude sees

Exactly what you may see in Tidande, and only when you ask. It is signed in as you, through your own
Google account; the plugin holds no password, key or data. Public data (the archive, the registries)
is served to anyone invited; investigations only as described in "Investigations" (your own, public
level, assistant access on).

## The audit log

Every call Claude makes to Tidande leaves one row: which tool, when, which investigation, ids of the
objects returned, how large the reply was, and a one-way hash of the arguments. Never the text of
your question. You see recent calls on the "Підключені застосунки" page, where you can also
disconnect at once.

## Once an answer is in a Claude chat

It is in your Claude account. Do not share such chats outside your newsroom, and keep model training
on your chats switched off in Claude's own privacy settings. Keep web-search and mail connectors out
of chats that use Tidande.

## Who may use what

- **Access** is by invitation into a Tidande workspace, sent by the owner. Without it every tool
  answers `no_access`, public data included.
- **The research level** is a second, separate permission the owner gives to named people. It adds
  the long-study command `/tidande:start-investigation` (Claude Code only) and the tools behind it:
  the Case Inventory (what was read and judged) and server-side triage of big candidate sets. Without
  it that command says so and stops; everything else works as for everyone. To ask for it, ask the
  owner of your Tidande workspace.
- Triage runs a small model on Tidande's own account and counts toward a daily limit; the command
  tells you when it is used.

## What Claude will not do

- Show a minor, a home address or health data, or use a private chat or leaked material. Give a
  verdict about a person or a company.
- Publish, export or share anything. Confirm a claim for you.
- Treat text inside a post or a web page as an instruction.
