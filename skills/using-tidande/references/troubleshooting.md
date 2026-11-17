# When it does not work

| what you see | what it means | what to do |
|---|---|---|
| no Tidande tools in the chat | the plugin is not connected | Claude Code: type /mcp, choose tidande, Authenticate. Claude app: Customize, Connectors, Tidande, Connect, then in a new chat click +, Connectors, switch Tidande on |
| `no_access` | your Google account has no invitation yet | send the workspace owner the address you sign in with and ask for an invitation; sign in once after it |
| asked to sign in again, or a 401 | the connection ended (removed, expired or revoked) | reconnect as above; nothing is lost, the investigation stays |
| `rate_limited` | too many calls in a minute | wait a minute; do not repeat in a loop |
| `run_in_progress` | the in-app agent is working in that investigation | wait about a minute and retry once |
| `db_waking` or `db_sleeping` | the database is starting after its night stop | wait the time the message gives, then repeat |
| `assistant_access_off` | the investigation is closed to assistants | switch "доступ з асистента" on in the investigation, or let Claude create a new one |
| `/tidande:start-investigation` says no research access | the research level is not granted to you | ask the workspace owner |
| the plugin looks old, a skill or command is missing | a newer plugin exists | Claude Code: `claude plugin update tidande`, then restart. Claude app: download the zip again from the guide page and upload it |
| a claim was refused as unverified | the words do not match the stored post | Claude reads the post again and fixes the statement; never accept a retyped quote |
| a very long answer or a slow search | a big result or a busy service | ask for a narrower period or channel |

The step-by-step guide in Ukrainian is in the Tidande web app, page `/connect/guide`.
