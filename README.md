# quartz-content

This repository stores the published content used by the Quartz site.

## What lives here

- Public Markdown notes
- `index.md`
- Public assets

## What does not live here

Do not put Quartz framework files here, such as:

- `package.json`
- `quartz.config.ts`
- `quartz.layout.ts`

Those belong to the main Quartz repository.

## Example structure

```text
quartz-content/
├─ index.md
├─ notes/
├─ assets/
└─ README.md
```

## Update content

```bash
git add .
git commit -m "Update published content"
git push
```

If this repo is used as a submodule, then update the pointer in the main Quartz repo:

```bash
cd ..
git add content
git commit -m "Update content submodule pointer"
git push
```

## Multi-device notes

If you clone this repo by itself, it works like a normal Git repo.

If you access it through the Quartz repo as `content/`, remember:

1. Commit and push here first
2. Then commit the submodule pointer in the main repo

## Notes

- Only keep content here that is safe to publish
- Private vault content should stay outside this repo
- If you later add automated syncing from your Obsidian vault, this repo can remain the public output repo
