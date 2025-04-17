---
id: README
title: The README of markdown-blog Repository
permalink: /
date: 2025-03-19 10:29:28
thumbnail: example_1.jpg
tags: [Markdown Blog, Guide]
---

- This file can be used as a template for a blog post.
- The [first 8 lines](https://raw.githubusercontent.com/CoderResume/markdown-blog/refs/heads/main/published/README.md) are metadata. The `id` is required, and the others can be omitted.

## Key 'id'

- `id` is **required**. Post will not be created on the blog without an `id`.
- For an `id` value, only upper and lower case letters, numbers, and `_` are valid. `-` will be replaced by `_`.
- If `id` contains invalid characters, the post will **not** be created.
- `id` should be **unique**. If multiple posts have the same `id`, only one post will be displayed on the blog.
- You can name the Markdown file anything you want. The file name doesn't matter because we mainly use `id` to identify a *post*.

## Key 'permalink'

### When 'permalink' is empty, '/', or invalid

- If the `permalink` value is empty, `/`, or invalid, we will automatically generate a `permalink` based on the value of `title`.
- For example, if the title is `This is an Example Post`, the corresponding permalink will be `this-is-an-example-post`. Spaces are replaced with `-`, illegal characters will be deleted, and uppercase letters are converted to lowercase letters.

### You can modify the 'permalink' at any time without worrying about SEO weight of the post being reduced.

- That's because we append a `-` and the `id` to the end of each post link.
    So for this post, the real URL would be like [https://your-domain.com/the-readme-of-markdown-blog-repository-README](https://your-domain.com/the-readme-of-markdown-blog-repository-README).
- Visiting a stale URL will be redirected to the fresh URL with status `301`.

## Key 'thumbnail'

- Files in the `jpg jpeg gif png` format in the [/images](/images) directory will be synchronized to the `/public/images` directory on the blog server.
- At the same time, the blog system will **automatically create a thumbnail** for each image. The naming rule is to add `_thumb` after the original image name, such as the thumbnail of `image_name.jpg` is `image_name_thumb.jpg`.
- To display the automatically generated thumbnail in your blog post, you can use `thumbnail: image_name.jpg`. In fact, the image used in the blog is `/images/image_name_thumb.jpg`.

## Categories

- Here, `categories` are **directories**, and they are **equivalent**. `posts` are placed in directories in the form of markdown files.
- No matter you name the directory `ruby_on_rails`, `Ruby_on_Rails`, `ruby-on-rails`, `Ruby-on-Rails`, `Ruby on Rails`, or `Ruby On rails`, from the blog's point of view, they are the same `category`. The category's URL path is `ruby-on-rails`, and the category's blog display name is `Ruby On Rails`.
- If a rename of directory causes the URL path to be changed, the original URL path will be inaccessible, and the new URL path will not inherit the SEO weight of the original URL path. To avoid this, we provide a URL 301 redirect function for directories in the `/admin` backend.

## Files

Any file format in the [/files](/files) directory will be synchronized to the `/public/files` directory on the blog server and can be referenced and downloaded in the blog.

For referencing a file, it is completely Markdown syntax, e.g., [empty example PDF](/files/empty_example.pdf).

## How to add pictures to your posts?

Remember to put the images in the [/images](/images) directory. The blog **cannot** recognize other directories as image directory!

For referencing an image, it is completely Markdown syntax, e.g.,

![](/images/example_1.jpg)

*A Little Penguin*

## What are the best practices for using markdown?

Please read [Markdown Guide ](https://markdownguide.offshoot.io/basic-syntax/).
