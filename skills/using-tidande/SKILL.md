---
name: using-tidande
description: Explains Tidande to a journalist who is new to it - what it holds, what Claude can do with it, what to ask for, how investigations, claims and proposals work, what is private, and what to do when something does not work. Use when someone asks how to use Tidande, what you can do, where to start, what Tidande has, or how to get access. Ukrainian requests too, e.g. "як користуватися Tidande", "що ти вмієш", "з чого почати", "що є в Tidande", "як це працює".
---

# Using Tidande (guide)

Answer in the person's language (Ukrainian by default), in plain words, for a journalist who may have
never used Claude Code. Do not call tools for this question except to check access (last section).
Give the short answer first, then offer to go deeper. Never invent a number, a date or a source: when
a detail is not in these files, say so.

## The short answer

Tidande is an archive of Ukrainian news sites and Telegram channels, joined to state registries
(companies, procurement, public money, courts, declarations, council and parliament votes). Claude
searches it for you, reads what it finds, and keeps findings in your own Tidande investigation as
proposals you review. Every quote is checked by code against the stored post.

## What to ask for

| you want | say, for example | skill |
|---|---|---|
| what was published, who was first, a timeline | "що писали про ремонт мосту, хто перший повідомив" | `researching-a-story` |
| is a quote real, where it was published | "перевір цитату ..." | `verifying-quotes-and-claims` |
| who owns a company, what a body bought | "хто власник ..., які тендери виграла ..." | `checking-companies-and-tenders` |
| a long, many-angled study (Claude Code, research access only) | `/tidande:start-investigation` and your question | `start-investigation` |

More example requests, by task: [references/requests.md](references/requests.md).

## What Tidande holds, and what it does not

Sources, registries, the period and the limits: [references/data.md](references/data.md). One rule to
say out loud whenever it matters: absence in our copy is not absence in the world. A reply says what
our copy holds (`coverage`, `notes`); report that, never "nothing happened".

## Investigations, claims and proposals

How they work and how to review them in the web app:
[references/investigations.md](references/investigations.md). In one line: Claude writes proposals,
you confirm; a preview is never a quote; a quote is a fragment of a stored post.

## Privacy, access and the research level

What Claude sees, the audit log, training settings, who may use what:
[references/privacy-access.md](references/privacy-access.md).

## When it does not work

[references/troubleshooting.md](references/troubleshooting.md): no access, sign in again, an old
plugin, slow answers.

## Check access, when the person says it fails

Call `investigations_list`. An answer means the connection works. `no_access` means no invitation
yet: the workspace owner sends it. No Tidande tool at all means the plugin is not connected: in
Claude Code type /mcp, choose tidande, Authenticate; in the Claude app open Customize, Connectors,
Tidande, Connect.
