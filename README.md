# Financial Thoughts

A personal finance blog built with GitHub Pages and Jekyll.

## Adding Articles

Create new markdown files in the `_posts/` folder. Filename format:

```
YYYY-MM-DD-{youtube_video_id}.md
```

Example frontmatter:

```yaml
---
layout: post
title: "Your Article Title"
date: 2026-01-20
category: Personal Finance
excerpt: "A short description of your article."
word_count: 500
channel_name: "Channel Name"
video_url: "youtube_video_id"
video_duration: "12:34"
---

**Note:** `video_url` should be just the YouTube video ID (e.g., `dQw4w9WgXcQ`), not the full URL. The HTML template automatically constructs the full YouTube link.

Your article content here...
```

## Local Development

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
