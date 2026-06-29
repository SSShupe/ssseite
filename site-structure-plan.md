# Site Structure Plan

## Directory Structure

```
content/
  posts/          # YYYY-MM-DD-slug.md  →  /posts/slug    (newest first)
  fiction/        # slug.md             →  /fiction/slug  (chapter order via weight)
  docs/           # YYYY-MM-DD-slug.md  →  /docs/slug     (newest first)
  pages/
    about.md      # →  /about
    links.md      # →  /links
    photos.md     # →  /photos
```

Photos, About, and Links are just files in `content/pages/` — they don't need their own collection. The current `content/photos/` directory (currently empty) can be left empty or removed.

---

## seite.toml Collections

Replace the four current `[[collections]]` blocks with:

```toml
[[collections]]
name = "posts"
label = "Posts"
directory = "posts"
has_date = true
has_rss = true
listed = true
url_prefix = "/posts"
paginate = 5
default_template = "post.html"

[[collections]]
name = "fiction"
label = "Fiction"
directory = "fiction"
has_date = false
has_rss = false
listed = true
url_prefix = "/fiction"
nested = false
default_template = "post.html"

[[collections]]
name = "docs"
label = "Documents"
directory = "docs"
has_date = true
has_rss = false
listed = true
url_prefix = "/docs"
nested = false
default_template = "doc.html"

[[collections]]
name = "pages"
label = "Pages"
directory = "pages"
has_date = false
has_rss = false
listed = false
url_prefix = ""
nested = false
default_template = "page.html"
```

Key changes from the previous config:
- `fiction` gets its own `directory = "fiction"` (was wrongly pointing at `"pages"`)
- `docs` gets `has_date = true` so it sorts newest first
- `photos` collection removed (replaced by `content/pages/photos.md`)
- `pages` added with `listed = false` — serves About/Links/Photos at root URLs but keeps them off the homepage listings

---

## Fiction: Oldest First

There is no `sort_order` config option documented for seite. The documented way to order a non-date collection is `weight` frontmatter (lower number = listed first). Each chapter gets:

```yaml
---
title: "Chapter 1: The Beginning"
weight: 1
---
```

```yaml
---
title: "Chapter 2: The Middle"
weight: 2
---
```

---

## data/nav.yaml

```yaml
- title: Posts
  url: /posts
- title: Fiction
  url: /fiction
- title: Photos
  url: /photos
- title: Documents
  url: /docs
- title: About
  url: /about
- title: Links
  url: /links
```
