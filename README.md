# Tidande for Claude

The Tidande plugin connects Claude to Tidande: the archive of Ukrainian news sites and Telegram
channels, the company and procurement registries, and your own Tidande investigations. Claude works
with exactly your Tidande access, and only after you sign in.

Tidande для Claude: пошук у новинах і Telegram-каналах, реєстри компаній і закупівель, ваші
розслідування з перевіреними цитатами. Claude бачить рівно те, що бачите ви в Tidande.

The step-by-step guide in Ukrainian is in the Tidande web app:
https://tidande-workspace-1060294906195.europe-central2.run.app/connect/guide

## Connect / Підключення

Access is by invitation. Without an invitation to a Tidande workspace Claude sees no data:
«немає доступу» → попросіть запрошення у власника робочого простору.

**Claude Code.** Paste one line into a terminal (PowerShell on Windows, Terminal on a Mac); if the
command is not recognised, run `claude update` first:

```
claude plugin install tidande --marketplace https://tidande-mcp-1060294906195.europe-central2.run.app/plugin/marketplace.json
```

Then start Claude Code, type `/mcp`, choose **tidande**, then **Authenticate**. The browser opens:
sign in with Google (the address that was invited), then click **Дозволити** (Allow).

**The Claude app** (claude.ai, desktop; uploading a plugin needs the Pro or Max plan, on the free
plan add the connector by hand, see the guide page). Download the plugin zip from the guide page (or
from https://tidande-mcp-1060294906195.europe-central2.run.app/plugin/tidande-claude-plugin.zip),
then **Customize → Plugins → Upload plugin** and choose the zip. In the plugin's **Connectors** tab
click **Add** next to Tidande if it shows "Not added", then **Connect**; sign in with Google and click
**Дозволити**. Then in a new chat click **+ → Connectors** and switch **Tidande** on; allow the first
Tidande tool call. A new plugin version means downloading and uploading the zip again.

**Check / Перевірка.** Ask Claude: «Пошукай у Tidande останні згадки про закупівлі Київської міської
ради і покажи джерела.»

**Disconnect / Відключення.** In Tidande open **Підключені застосунки** (Connected apps) and click
**Відключити**: the connection stops at once. Then remove the plugin: Customize → Plugins in the app,
or `claude plugin uninstall tidande` in Claude Code.

## Skills / Навички

| Skill | What it does |
|---|---|
| `researching-a-story` | What was written about a topic, who reported first, the chronology, the gaps; findings kept in your investigation |
| `verifying-quotes-and-claims` | Checks a quote against the stored post and keeps it as a claim with its exact fragment |
| `checking-companies-and-tenders` | Companies, founders, tenders, contracts and buyers from the state registries |

The skills only guide Claude; the work is done by the Tidande server's tools, which check every
quote against the stored text in code.

## Privacy / Приватність

- Claude sees only what you may see in Tidande, and only when you ask. Every call is recorded in
  Tidande's audit log (which tool, when; never the content of your question).
- What Claude writes into Tidande is a proposal you review; quotes are verified by code.
- Once an answer is in a Claude chat it is in your Claude account: do not share such chats outside
  your newsroom, and keep model training on your chats turned off in Claude's privacy settings.
- The plugin holds no data, no keys and no passwords; the sign-in happens in your browser.
