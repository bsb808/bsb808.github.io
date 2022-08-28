---
title:  "First post! Github pages and Jekyll."
last_modified_at: 2022-08-19T14:46:02-07:00
categories: git jekyll
---

This is definitely experimental. I am looking for lightweight infrastructure to support content that is more mature than my personal notes and less refined than a publication - often a place for me to document an intermediate working state of a project.

So, I'm taking [GitHub Pages](https://pages.github.com/) with [Jekyll](https://jekyllrb.com/docs/github-pages/) for a spin.

Setting up my user space on GitHub Pages is straightforward, resulting static webpage [bsb808.github.io/](https://bsb808.github.io/).  Then following the [GitHub Pages site with Jekyll](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll), which requires some host setup/installs - i.e., [install Jekyll](https://jekyllrb.com/docs/installation/ubuntu) and `bundle install`.  

From there, the workflow seems pretty simple...

## Add a post or page

Add a markdown text file to either the `_posts` directory (blog posts)  or the root (pages) as described in the [Add content to Pages site](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/adding-content-to-your-github-pages-site-using-jekyll) tutorial.  

## Try it locally first

From the project's root directory, start the local server...
```
 bundle exec jekyll serve
```

Then navigate to [http://localhost:4000](http://localhost:4000).