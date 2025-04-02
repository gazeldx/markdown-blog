---
id: x7Iwq
permalink: /
title: This is an Example Post 2
date: 2025-03-09 07:42:28
tags: [Markdown, Best Practices]
---

## Key 'id'

- `id` is **required**. Post will not be created on the blog without an `id`.
- `id` should be **unique**. If multiple posts have the same `id`, only one post will be published on the blog.
- For an `id` value, upper and lower case letters, numbers, and `_` are valid.

## Key 'permalink'

### When 'permalink' is Empty, '/', or Invalid

- If the `permalink` value is empty, `/`, or invalid, we will automatically generate a `permalink` based on the value of `title`.

	For example, if the title is `This is an Example Post`, the corresponding permalink will be `this-is-an-example-post`.

	Spaces are replaced with `-`, illegal characters will be deleted, and uppercase letters are converted to lowercase letters.

	Next time you modify the `title`, the value of `permalink` will also change accordingly.

### You can modify the 'permalink' at any time without worrying about SEO weight of the post being reduced.

- That's because we append a `-` and the `id` to the end of each post link.

	So for this post, the real URL would be like https://your-domain.com/this-is-an-example-post-x7Iwq

- Visiting a stale URL will be redirected to the fresh URL with status `301`.

## How to add pictures to your posts?

Remember to put the images in the [/images](/images) directory. The blog **cannot** recognize other directories as image directory!

For referencing an image, it is completely Markdown syntax.

![](/images/example_1.jpg 'A Little Penguin')

## What are the best practices for using markdown?

Please read [Markdown Guide ](https://markdownguide.offshoot.io/basic-syntax/).
