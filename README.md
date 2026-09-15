# Coveo knowledge transfer roadmap

A single-page roadmap for handing over the Coveo indexing pipeline and dashboard
configuration. Eleven modules, two progress tracks: one side marks a topic as
explained, the other sets their own level once they can do it unaided.

## Files

| File | Purpose |
|---|---|
| `index.html` | The page. No build step, no dependencies to install. |
| `coveo-kt-tracker.xlsx` | Topics **and** progress. The only source of both. |

The page carries no built-in topic list. Until the workbook is read it shows an
empty state asking you to connect or open a copy, so what you see is always what
is committed. It also refuses to commit or export while nothing is loaded, which
stops an empty board overwriting the workbook.

## Publish on GitHub Pages

1. Commit both files to the repository root.
2. **Settings → Pages →** deploy from a branch, folder `/ (root)`.
3. Open the published URL. The page fetches `coveo-kt-tracker.xlsx` from the same
   folder and draws the roadmap.

## Keeping progress in the repository

### Connected: commits happen for you

Open the **Connection** tab. Owner (`akshay0828`), repository (`CoveoKT`),
branch and workbook path come prefilled, so normally you just paste a token and
press **Connect**. From then on every mark is committed
to the workbook about four seconds after you make it, and the banner reports the
result. The page also re-reads the workbook whenever you come back to the tab, so
you pick up the other person's commits.

The token must be a **fine-grained personal access token**, scoped to **only this
repository**, with **Contents: Read and write** and nothing else. Give it the
shortest expiry you can live with.

- **Remember on this device** (on by default) keeps the token in that browser so
  you connect once. Switch it off and the token is held for the session only,
  while the repository details stay filled in. **Forget token** clears the token
  and leaves the details.
- The token is held in that browser only, under its own storage key. It is never
  written into the workbook, the exports or any commit.
- Anyone who can use that browser profile can use the token. Don't connect on a
  shared machine, and use **Forget token** when you are finished.
- Each person needs their own token and write access. Don't pass one around.
- If a token ever lands in a commit, a log, a screenshot or a chat, revoke it on
  GitHub immediately.
- Commits are attributed to the token's owner, so the history shows who changed
  what.

If two people save at once, GitHub rejects the second commit; the page re-reads
the file, merges, and commits again by itself.

### Not connected: save and commit by hand

1. Mark progress on the page.
2. Click **Save to Excel**. It downloads `coveo-kt-tracker.xlsx` with the
   progress columns filled in.
3. Commit that file over the old one.

Editing the workbook directly in Excel works equally well — the page reads
whatever is committed.

Saving from the page rewrites the workbook through a JavaScript library, so cell
fills and fonts from the original are not carried over. The data is.

## Editing the topic list

Columns A–G are content, H–L are progress. Add, remove, reorder and reword rows
freely. Two rules:

- Keep the header row exactly as it is. Columns are matched by header name.
- `Topic` is the identity of a row. Renaming one restarts its progress.

`Stage goal` is filled on the first row of a module and left blank on the rest.
`Confidence` is one of: Not started, Following along, Can do with help, Can do it
solo. A topic counts as signed off only when `Explained` is Yes **and**
`Confidence` is Can do it solo.

## Configuration

Two constants near the top of `index.html`:

- `REPO_FILE` — the workbook to read. A `.csv` file also works; the extension
  decides how it is parsed.
- The SheetJS `<script>` tag, loaded from cdnjs. If your network blocks it,
  commit `xlsx.full.min.js` beside `index.html` and point the `src` at it.
  Without it the page still runs but cannot read or write `.xlsx`.

## On a public repository

The page and the workbook are readable by anyone. Keep organization IDs, source
IDs, endpoint URLs, key names and key values, store names and client identifiers
out of both; reference the private runbook instead. If a key ever lands in a
commit, rotate it.

Licence names and scope in module 1 came from the handover brief and are
unexpanded — confirm them with the account owner. Rows pointing at "Internal"
resources are prompts to fill in from our own runbook.
