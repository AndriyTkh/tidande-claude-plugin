# What Tidande holds

## The post archive

News sites and Telegram channels, collected for a pilot year. The exact first and last day are not
fixed in this guide: every `search` reply and its `coverage` block carries the period, so say it from
the reply. A question outside the period gets that answer, not a guess.

- Search works by meaning and by exact words together. Exact names and phrases work best with the
  exact spelling, in Ukrainian or Russian.
- A search hit shows a short preview. A preview is for choosing what to read, never a quote. Claude
  opens the post (`get_post`, `get_posts`) before it quotes.
- Posts can be edited or deleted after collection. Claude says which version it read.
- Sources differ: an outlet that repeats another is not a second source. Claude separates the first
  report from reposts when asked.

## Registries (our copy, with the load date in each reply)

| area | what is in it |
|---|---|
| companies | the state register of legal entities: owners, founders, related companies; sanctions lists; bankruptcy notices, debtors, shareholders, natural monopolies |
| procurement | Prozorro tenders, awards, contracts and their changes, plans, documents, who bid together, unit prices |
| public money | treasury payments and contracts (treasury accounts only), budget plan against actual per programme, chains from payer to supplier |
| courts | court decisions that name a company's code |
| declarations | asset declarations of officials, by public role; minors are never shown |
| councils and parliament | Kyiv City Council decisions and roll-call votes; Verkhovna Rada votes |

Every registry reply says which source it read, what that source covers at all, the dates our copy
holds and when it was loaded. Read the `coverage` and `notes` fields: for example, a payment through a
commercial bank is not in treasury data, so "no treasury payment" is not "no payment".

## Limits to state plainly

- Absence in our copy is not absence in the world.
- Names of private persons are masked or refused in most views; people appear in their public role.
  On a closed research deployment the owner can switch masking off; replies then say so
  (`unmasked`), and nothing from them is for publication in that form.
- Web pages Claude finds elsewhere are leads, never evidence: a claim needs a stored post fragment or
  a registry record.
- Claude publishes or shares nothing. Export and sharing are yours.
