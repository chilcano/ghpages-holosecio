---
title: "From a WordPress.com's blog to Jekyll and then to Hugo"
date: 2021-06-20T20:00:00+02:00
draft: false
type: post
layout: single_simple
categories: [Misc, CMS]
tags: [Github, Wordpress, Jekyll, Hugo, Go]
comments: true
url: /2021/06/20/from-wordpress-blog-to-jekyll-and-then-to-hugo
---

I promise, I won't change it again. I had (still have it) my first blog on [WordPress.com](https://holisticsecurity.wordpress.com) but I migrated it to [GitHub Pages](https://pages.github.com) using [Jekyll](https://jekyllrb.com), after 2 years using it I made the decission to replace Jekyll for [Hugo](https://gohugo.io). 

The decision was made based on these points:
* I didn't want waste my time fixing Ruby (Jekyll) dependencies every time I wanted to write a new blog post.
* I wanted to continue using Github Pages with the same workflow and reuse previous published content.

![](/assets/img/20210620-from-wordpress-to-jekyll-then-to-hugo.png)

<!--more-->

## Process

### 1. Migrate a Blog from WordPress.com to GitHub Pages using Jekyll

To do that, just follow next 2 articles:
* [Migrating WordPress.com's blog to GitHub Pages with Jekyll - Part 1](/2019/10/14/migrating-wordpress-com-blog-to-github-pages-with-jekyll-part1)   
  This article explains how to export WordPress.com's blog and serve a static website in GitHub Pages using a Jekyll.
* [Migrating WordPress.com's blog to GitHub Pages with Jekyll - Part 2](/2019/12/10/migrating-wordpress-com-blog-to-github-pages-with-jekyll-part2)   
  This 2nd article explains how to customize the recently created static website: Themes, Layouts, Pagination and Excerpts, also, I'm sharing a Python script to convert HTML post files to Markdown. 

### 2. From Jekyll to Hugo

Once migrated your blog to GitHub Pages and if you want to change Jekyll to Hugo, follow next steps.


#### 2.1. Pre-requisites

This script installs `git`, `hub`, configures git and authentication method, tests `hub`, etc.
```sh
source <(curl -s https://raw.githubusercontent.com/chilcano/how-tos/master/src/git_and_hub_setting_in_linux.sh) \
  -u=Chilcano \ 
  -e=chilcano@intix.info
```
This script installs latest Hugo CLI (`hugo`)
```sh
curl -s https://raw.githubusercontent.com/chilcano/how-tos/master/src/hugo_setting_in_linux.sh | bash
```

#### 2.2. Convert the Jekyll website to Hugo content

You have to go along below steps:
1. Clone/download existing Jekyll GitHub Pages site.
2. Import existing downloaded site using Hugo CLI.
3. Run the site locally using Hugo CLI.
4. Migrate existing Jekyll theme or download new Hugo theme.
5. Re-run the site locally using Hugo CLI.
6. Publish the Hugo site on a GitHub Pages new repository.
7. Configure the published GitHub Pages Hugo site.
8. Check everything!

But if you don't want to go through above steps manually, no worries, I've created a bash script to do everything automatically, only you have to run below command:

Running the script in this way (`source <(curl -s https://url-to-my-bash) --my-params`), we will run the bash in the current shell context which allow us to change directory. This script also will publish the imported site to GitHub in Hugo format.
```sh
source <(curl -s https://raw.githubusercontent.com/chilcano/how-tos/master/src/migrate_jekyll_to_hugo.sh) \ 
  --help

source <(curl -s https://raw.githubusercontent.com/chilcano/how-tos/master/src/migrate_jekyll_to_hugo.sh) \
  --ghuser=<github_usr> \ 
  --source_url=https://github.com/<usr>/<jekyll_repo> \ 
  --destination=<dir> \ 
  --theme=<hugo_theme>
```

Where:
* `--ghuser` or `-u`: The GitHub user.
* `--source_url` or `-s`: The website URL that we are going to migrate to Hugo.
* `--destination` or `-d`: The GitHub repository name that will contain the migrated website.
* `--theme` or `-t`: The theme name that the Hugo website will use. The theme is downloaded from Hugo Themes website.

```sh
source <(curl -s https://raw.githubusercontent.com/chilcano/how-tos/master/src/migrate_jekyll_to_hugo.sh) \ 
  -u=chilcano \ 
  -s=https://github.com/chilcano/ghpages-holosec.git \ 
  -d=site01 \ 
  -t=hugo-theme-cactus 
```

I'm using this directory structure:
```sh
$ tree . -d -L 4 -I 'docs|resources|blog20*'
.
├── ghp-content
└── ghp-scripts
    ├── content
    │   └── post
    ├── layouts
    │   ├── _default
    │   ├── partials
    │   ├── post
    │   └── shortcodes
    ├── static
    │   ├── assets
    │   │   ├── _old_
    │   │   ├── img
    │   │   └── pages
    │   ├── blog
    │   ├── css
    │   └── images
    └── themes
        └── hugo-theme-cactus
            ├── exampleSite
            ├── images
            ├── layouts
            └── static

23 directories
```

Bear in mind these considerations:
- The `config.toml` file is under `ghp-scripts/`.
- The new `content`, `layout`, `static` and `themes` must be created under `ghp-scripts/`.
- Before publishing the new content, it must be generated running `hugo` command from `ghp-scripts/`. The generated content will be generated under `ghp-content/docs/`.


#### 2.3. Serving Hugo content and publishing content


To server the site locally you have to run `hugo serve` command from `ghp-scripts/` folder. The content will be generated in memory. 
```sh
hugo server -D --bind=0.0.0.0 --baseURL=http://<your_hugo_ip_address>:1313/
```
Changing the directory, running the above command, going back to parent directory to run another git commands is annoying, to relef this I created a bash 2 scripts, both can be executed from parent directory.  

You can download below bash scripts in the root of your cloned Hugo website and execute from there.

##### Script to server the Hugo content locally

```sh
source <(curl -s https://raw.githubusercontent.com/chilcano/how-tos/master/src/hugo_run_locally.sh) 
```

##### Script to publish Hugo content to GitHub Pages

```sh
source <(curl -s https://raw.githubusercontent.com/chilcano/how-tos/master/src/hugo_publish_site.sh) \ 
  --commit_msg=my-message | -m=my-message
```

That's all. Hope this is useful.
