---
title: The blog
image:
  caption: "Posts"
  focal_point: ""
  preview_only: false
---

- block: collection
    id: posts
    content:
      title: Posts
      subtitle: ''
      text: ''
      # Choose how many pages you would like to display (0 = all pages)
      count: 5
      # Filter on criteria
      filters:
          folders:
            - post
      author: "jpgoldberg"
      # category: ""
      # tag: ""
      exclude_featured: false
      exclude_future: false
      exclude_past: false
      publication_type: ""
      # Choose how many pages you would like to offset by
      offset: 0
      # Page order: descending (desc) or ascending (asc) date.
      order: desc
    design:
      # Choose a layout view
      view: compact
      columns: '2'
