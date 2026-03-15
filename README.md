# Financial Thoughts

A personal finance blog built with GitHub Pages and Jekyll.

## dummy trigger

## Adding Articles

Create new markdown files in the `_posts/` folder with this naming convention:

```
YYYY-MM-DD-article-title.md
```

Example frontmatter:

```yaml
---
layout: post
title: "Your Article Title"
date: 2026-01-20
category: Personal Finance
excerpt: "A short description of your article."
---

Your content here...
```

## Local Development

To preview locally, install Jekyll:

```bash
gem install jekyll bundler
bundle install
bundle exec jekyll serve
```

Then visit `http://localhost:4000`

## Deploying

1. Push to GitHub
2. Go to Settings → Pages
3. Select "main" branch as source
4. Your site will be published automatically
