# Editing — Taha Ayub's One Pager

A complete walkthrough for editing this site. Bookmark this file.

## 1. Open the file

Right-click `index.html` → **Open with** → **Notepad** (or **VS Code** if you have it — free at https://code.visualstudio.com — strongly recommended; it highlights syntax and previews Markdown).

## 2. Find what to edit

Press `Ctrl+F` and search for **`EDIT:`** — every editable spot has a comment like `<!-- EDIT: your name -->` directly above the line to change. Hop through matches with `F3`.

## 3. Make the change

Change only the text **between** the tags, never the tags themselves.

| Goal | Find this marker | What to change |
|---|---|---|
| Your name | `EDIT: your name` | text inside `<h1>...</h1>` |
| Role / eyebrow | `EDIT: role / eyebrow line` | text inside `<p class="eyebrow">...</p>` |
| Tagline | `EDIT: tagline / team` | text inside `<p class="tagline">...</p>` |
| Email | `EDIT: email` | **both** the `mailto:` address AND the visible text |
| Phone | `EDIT: phone` | digits in `href="tel:..."` AND visible number |
| Location | `EDIT: location` | text after `<span class="label">Location</span>` |
| Background | `EDIT: background paragraphs` | text inside `<p>...</p>` blocks |
| A skill | `EDIT: skills` | text inside any `<li>...</li>` |
| A cert | `EDIT: certs` | text inside any `<li>...</li>` |
| A role bullet | inside any `<article class="role">` | text inside `<li>...</li>` |

**Add a new skill, cert, or bullet:** copy a whole `<li>...</li>` line, paste it just below, edit the text.
**Remove one:** delete the entire `<li>...</li>` line.

## 4. Add or remove a whole job

In the *Selected Client Experience* section, each job is one block:

```
<article class="role">
  ...
</article>
```

**Add a job:** copy the whole block (from `<article` to `</article>`), paste where you want it in order, edit company, role title, and bullets.
**Remove a job:** delete the entire block.

## 5. Replace the photo

Just drop a new image into `C:\Users\taha.ayub\Projects\tayub-accenture.github.io\` **named exactly `photo.jpg`** (overwrite the existing one). No code change needed.

- Square-ish photo, 400×400 px or larger looks best
- JPG or PNG both work
- If you want a different filename instead, find `EDIT: photo` in `index.html` and change `src="photo.jpg"` to the new name

## 6. See your changes locally

1. Save the file (`Ctrl+S`)
2. Refresh the browser tab showing `index.html` (`Ctrl+R`)

That's it for local previewing. Iterate as much as you want before publishing.

## 7. Publish to the live site

Open PowerShell, then run (you can copy-paste all four lines at once):

```powershell
cd C:\Users\taha.ayub\Projects\tayub-accenture.github.io
git add .
git commit -m "Update resume"
git push
```

GitHub Pages redeploys automatically in ~30–60 seconds. Hard-refresh the live URL with `Ctrl+Shift+R` to see it:

**https://tayub-accenture.github.io/**

## Safety net — undo uncommitted changes

If an edit breaks the page and you want to throw away everything you've changed since the last publish:

```powershell
cd C:\Users\taha.ayub\Projects\tayub-accenture.github.io
git restore .
```

This snaps every file back to the last committed (live) version. The photo file is also versioned, so this works for the photo too.

## Roll back the live site

If you published something bad and want the *live* site to revert to the previous version:

```powershell
cd C:\Users\taha.ayub\Projects\tayub-accenture.github.io
git log --oneline
```

That prints recent commits. Copy the short hash of the commit you want to go back to, then:

```powershell
git revert <hash>
git push
```

This creates a new commit that undoes the bad one, and re-publishes. Safer than rewriting history.

## Common gotchas

- **Don't put `<!-- ... -->` inside another `<!-- ... -->`.** HTML comments can't nest — the inner `-->` ends the outer comment, leaking text onto the page. (This is what happened on first deploy.)
- **Keep tags balanced.** Every `<p>` needs a `</p>`, every `<li>` needs a `</li>`. If the page renders weirdly, this is the usual cause.
- **Use straight quotes, not smart quotes.** If you copy from Word, it may insert curly quotes (`"` and `"`) in attributes like `href="..."`. Always type quotes directly in the editor.
- **Don't rename `index.html`.** GitHub Pages requires a file with exactly that name at the project root.
