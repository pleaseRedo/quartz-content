# quartz-content

This repository stores the **published content** used by the Quartz site.

It is mounted into the main Quartz repo as the `content/` submodule.

---

## What belongs here

- public Markdown notes
- public `assets/` folders
- manually maintained `index.md`
- `README.md`

## What does not belong here

Do not put Quartz framework files here, such as:

- `package.json`
- `quartz.config.ts`
- `quartz.layout.ts`
- Quartz plugins / theme code

Those belong to the main Quartz repo.

---

## Structure

A typical structure looks like this:

```text
quartz-content/
├─ index.md
├─ 03-Reference/
├─ notes/
├─ assets/
└─ README.md
```

The exact folder layout mirrors the original relative paths from the private Obsidian vault for notes tagged with `blog`.

---

## How content gets here

This repo is **not** edited manually most of the time.

The normal flow is:

1. write notes in the private Obsidian vault
2. tag publishable notes with `blog`
3. run the sync script from the main Quartz repo
4. the script mirrors matching notes into `content/`
5. commit and push this repo
6. commit and push the updated submodule pointer in the main Quartz repo

---

## Publish tag

A note is published only if its frontmatter tags contain `blog`.

Examples:

```yaml
---
title: My Note
tags: [blog]
---
```

```yaml
---
title: My Note
tags:
  - blog
---
```

```yaml
---
title: My Note
tags: blog
---
```

Inline body tags like `#blog` are **not** used as the publish trigger.

---

## Manual files that are preserved

These files are intentionally preserved during sync:

- `README.md`
- `index.md`

`index.md` is maintained manually and acts as the site homepage.

---

## Working with this repo

In normal daily use, you should work through the submodule path inside the main Quartz repo:

```text
quartz/content
```

That means the practical commands are usually run from inside the submodule directory under the main repo, not from a second separate local clone.

### Commit content changes

```powershell
cd .\content
git status
git add .
git commit -m "Sync blog notes from vault"
git push
```

Then go back to the main repo and update the submodule pointer:

```powershell
cd ..
git add content
git commit -m "Update content submodule pointer"
git push
```

---

## New machine notes

If you clone the main Quartz repo with:

```bash
git clone --recurse-submodules <repo-url>
```

then this repo will appear as:

```text
quartz/content
```

That submodule working copy is the recommended place to commit content updates.

---

## Common mistakes

### 1. Pushing this repo but not updating the main repo pointer

After content is pushed, the main Quartz repo still needs:

```powershell
cd ..
git add content
git commit -m "Update content submodule pointer"
git push
```

### 2. Keeping a second active local clone

Avoid maintaining a second active local working copy of this repo for day-to-day publishing. It makes sync and branch state harder to manage.

### 3. Expecting non-`blog` notes to appear here

Only notes selected by the sync rules are mirrored here.

---

## Summary

This repo is the public content layer.

- private Obsidian vault = source of truth
- `quartz-content` = published content repo
- `quartz` = site framework and deployment repo

In practice, update this repo through the `quartz/content` submodule working copy, then update the main repo pointer.