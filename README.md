# EMC-Support-Resources
Repo for support web page and rousources

This repository holds all content for the EMC Support site. The support site (built in Lovable) reads from this repo, so **editing content here updates the live site** — no developer or code changes needed.

> **Important:** This is a **public** repository. Never commit anything sensitive — no passwords, API keys, personal/private data, or internal-only documents. Only non-sensitive help content belongs here. Anything committed remains in the history even after deletion.

---

## How the site decides what to show

Two things control what a visitor sees:

1. **What content exists** — every file in `content/` is a possible piece of content.
2. **Who the visitor is** — the site reads an `org` from the link the visitor used (e.g. `?org=garland-isd`). It then shows content tagged for that org, **plus** anything tagged `all`.

So content tagged `all` is universal (everyone sees it). Content tagged with a specific org (e.g. `garland-isd`) only shows to visitors from that org. A visitor with no org sees only `all` content.

---

## Folder structure

```
config/        Site settings — org contact info, products (orgs.json)
content/       One file per article / training item / FAQ
assets/        Images and downloadable files (PDFs, etc.)
```

- **Filenames are permanent.** The filename becomes part of the link to that content. Renaming a file breaks existing links. Use lowercase-with-hyphens and choose a name that will last.

---

## How to add or edit content

All editing is done on the GitHub website — no software to install.

### To edit an existing item
1. Open the file in `content/`.
2. Click the pencil (Edit) icon.
3. Make your changes.
4. Add a short note describing the change and click **Commit**.

### To add a new item
1. In `content/`, click **Add file → Create new file**.
2. Name it `content/your-item-name.md`.
3. Paste the template below, fill it in, and commit.

### To hide an item without deleting it
Set `published: false` in its frontmatter. It stays in the repo but disappears from the site. This is how you draft something before it's ready.

---

## Article template

Every file starts with a frontmatter block between `---` lines, followed by the content.

```markdown
---
title: "Your Title Here"
orgs: ["all"]
product: "ccmr-weekly-workbook"
category: "Training"
group: "CCMR Weekly Workbook"
order: 1
type: "article"
link: ""
published: true
---

Your content goes here in Markdown.
```

### Field reference

| Field | What it does |
|-------|--------------|
| `title` | The display title shown on the site. |
| `orgs` | Who sees it. `["all"]` = everyone. `["garland-isd"]` = only Garland. Can list multiple: `["garland-isd", "other-isd"]`. |
| `product` | Which product it relates to (e.g. `ccmr-weekly-workbook`). |
| `category` | Top-level grouping (e.g. `Training`). |
| `group` | Sub-grouping within a category — this is the expandable header (e.g. `CCMR Weekly Workbook`). |
| `order` | Number controlling sort position within its group (lower = higher up). |
| `type` | `video` (opens a video link), `document` (opens a PDF/doc link), or `article` (content shown inline from the body below). |
| `link` | The URL for `video` and `document` types. Leave empty for `article`. |
| `published` | `true` shows it; `false` hides it. |

---

## Editing org settings (contact info)

`config/orgs.json` holds each org's display name, contact info, and products. To update a contact or add an org, edit this file. Use a **role-based email alias** (e.g. `garland-support@...`) rather than a personal email where possible, so the address doesn't need to change when staff change.
## Onboarding a new org
 
None of these steps require a developer or any code changes.
 
1. **Add the org to `config/orgs.json`.** Copy an existing org block (e.g. `garland-isd`), rename the key to the new org's slug (lowercase, hyphens, e.g. `plano-isd`), and fill in their `displayName`, `contact` info, and `products` list.
2. **Tag any org-specific content.** If the new org uses an existing product whose content is tagged `all`, do nothing — they inherit it automatically. Only edit content files if the org has its own bespoke material; in that case add their slug to that file's `orgs` array (e.g. `orgs: ["plano-isd"]`).
3. **Create their link.** The org is reached at `yoursite.com/?org=their-slug` (e.g. `yoursite.com/?org=plano-isd`). Give this link to whoever embeds it in the org's workbook or materials.
That's the whole technical onboarding. The real effort is only in **authoring new content** — and only when the org uses a genuinely new product. An org using an existing product needs no new content at all.
 
---
 
## Adding a product to an existing org
 
1. **Add the product** to that org's `products` array in `config/orgs.json`.
2. **Add the product's content files** to `content/`, tagged `all` if every org with that product sees the same material, or the org's slug if it's their custom version. Give them a new `group` value (e.g. the product's name) — the site will show it as its own expandable section automatically.
---
 
## What requires a developer (the boundary)
 
- **Adding more content of existing types** (`video`, `document`, `article`) → just files. No developer.
- **Adding a brand-new *kind* of content** the site doesn't render yet (e.g. an interactive tool, a new format) → this needs a code change in the app. Flag it to the developer.
