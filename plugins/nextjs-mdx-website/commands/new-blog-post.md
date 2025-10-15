---
name: new-blog-post
description: Create a new MDX blog post with proper frontmatter and structure
---

# New Blog Post

Creates a new MDX blog post in the `content/blog/` directory with proper frontmatter and structure.

## Usage

/new-blog-post [title]

## What This Does

1. Creates a new MDX file in `content/blog/` with kebab-case filename
2. Adds complete frontmatter with:
   - Title
   - Excerpt
   - Date (today)
   - Author information
   - Category and tags
   - Reading time estimate
3. Provides basic MDX structure with examples

## Examples

```
/new-blog-post How to Deploy Next.js to Vercel
```

Creates: `content/blog/how-to-deploy-nextjs-to-vercel.mdx`

## Frontmatter Template

The command uses this MDX frontmatter structure:

```mdx
---
title: "Your Post Title"
excerpt: "Brief description for SEO and previews"
date: "2025-01-29"
author:
  name: "Author Name"
  image: "/headshot.jpeg"
category: "Technology"
tags: ["nextjs", "typescript", "deployment"]
image: "/blog/hero-image.jpg"
featured: false
readTime: 5
---

## Introduction

Your content here...

## Main Content

More content...

## Conclusion

Wrap up...
```

## Requirements

- Project must have `content/blog/` directory
- Images should be placed in `public/blog/`
