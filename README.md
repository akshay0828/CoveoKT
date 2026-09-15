# Coveo knowledge transfer roadmap

A single-page roadmap for handing over the Coveo indexing pipeline and dashboard
configuration. Eleven modules, two progress tracks: one side marks a topic as
explained, the other sets their own level once they can do it unaided.

## Files

| File | Purpose |
|---|---|
| `index.html` | The page. No build step, no dependencies to install. |
| `coveo-kt-tracker.xlsx` | Topics **and** progress. The only source of both. |

The page carries no topic list of its own and no local-file fallback. The
**Roadmap** tab stays disabled until the workbook has been read from the
repository, so what you see is always what is committed. It also refuses to
commit or export while nothing is loaded, which stops an empty board overwriting
the workbook. **Forget token** closes the roadmap again.

The workbook has four sheets:

- `Roadmap` — topics in columns A–G, progress in H–L. Column L is a read-only
  summary of the question threads, e.g. "1 open of 2".
- `Links` — reference material per module, one row per link. `Stage` must match
  a `Stage` value on the Roadmap sheet exactly.
- `Questions` — one row per message. A `Question` row followed by its `Comment`
  rows, grouped by `Topic` and `Thread`. `Status` is `Open` or `Clear`.
- `People` — the two names in the page header, under `Explaining` and `Learning`.
- `How to use` — the notes above, in the file itself.

## Reference material

Each module carries a strip of saved links above its topics. The explainer adds
them with **Add links** — a name, a link or a pointer such as "Internal -
runbook", and an optional line on why it matters. The learner sees the strip and
can open anything on it, but cannot change the list. Only `http` and `https`
addresses become clickable; anything else is kept as plain text, and a bare
domain gets `https://` added for you.

## Roles and signing in

**Learner** is the default: set your own confidence level, ask questions, and mark
one clear when it is. **Explainer** marks topics as explained, answers questions,
and edits the content — it asks for a user name and password, both `admin` by
default, set as `ADMIN_USER` and `ADMIN_PASS` near the top of `index.html`.

Those credentials stop the learner editing the roadmap by accident. They are not
security: the page is public, so anyone can read them in the source. Never put a
real password there, and don't rely on it to protect anything.

## Editing the content (explainer mode)

- **Edit** on any topic row opens its name, what to cover, type, resource and
  note, with a delete option. Renaming a topic carries its progress and its
  question threads across.
- **Add a topic to this module** at the foot of each module, and **Add a module**
  at the foot of the board.
- **Edit module** renames a module or rewrites its goal; deleting one removes its
  topics and their progress, after a confirmation.
- **Add links** keeps the reference material for a module — label, address and an
  optional note. Only `http` and `https` addresses become clickable.

Content edits commit like any other change, and a pull will not overwrite edits
you have not committed yet.

## Questions and answers

The **Anything still unclear?** button on each topic opens a thread editor. The
learner adds questions one at a time and decides when one is clear; the explainer
adds comments underneath. Marking a question clear is the learner's call, so the
explainer sees the status but cannot change it — switch **Editing as** to *Both*
when you are working through them together. Open questions raise a flag on the
topic row and show a count on the button.

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

### Saving a copy by hand

**Save to Excel** downloads the same workbook, progress and names included, if
you want a copy or need to commit it yourself. Editing the workbook directly in
Excel works equally well — the page reads whatever is committed.

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
