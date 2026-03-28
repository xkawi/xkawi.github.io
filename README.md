# xkawi
this repo contains information about me - [xkawi.github.io](http://xkawi.github.io)

## Testing locally

This site is built with [Jekyll](https://jekyllrb.com) and hosted on GitHub Pages.

**Prerequisites:** Ruby ≥ 3.0 and Bundler.

```bash
# Install dependencies (first time only)
gem install bundler
bundle install

# Start the dev server
bundle exec jekyll serve
```

Open [http://localhost:4000](http://localhost:4000). The server watches for file changes and rebuilds automatically — just refresh the browser.

## Writing articles

Add a file to `_posts/` following the `YYYY-MM-DD-slug.md` naming convention:

```markdown
---
title: "Your Article Title"
description: "One-line summary shown on the home page and articles listing."
tags: [JavaScript]
---

Your markdown content here...
```

The home page automatically shows the 3 most recent posts. All posts are listed at `/articles/`.
