---
categories: [Misc, CMS]
comments: true
date: "2019-10-14T15:58:00Z"
tags: [Github, Wordpress, Jekyll, Python]
title: Migrating WordPress.com's blog to GitHub Pages with Jekyll - Part 1
url: /2019/10/14/migrating-wordpress-com-blog-to-github-pages-with-jekyll-part1
type: post
layout: single_simple
---
I would like to share my experience migrating my blog site hosted in WordPress.com to GitHub Pages in 2 parts.
In this blog post (Part 1) I will explain how to use Jekyll to export/import, how to configure GitHub Page site to host a fully blog as a headless Content Management System (CMS) based on Ruby. 
In the next blog post (Part 2) I will explain how to manage the look&feel, layouts, etc.
![Migrating WordPress.com's blog to GitHub Pages by using Jekyll](/assets/img/2019-10-14-blog-migration-wp-github.png)

<!--more-->

## Create a GitHub Pages repository

I created an empty GitHub repository, in my case is [`ghpages-holosec`](https://github.com/chilcano/ghpages-holosec), to host my migrated WordPress.com's blog, then I followed the [https://pages.github.com](https://pages.github.com) guide and configured it as `Project site`, no as `User or organization site` since my GitHub Account will host multiple Sites with different custom Domain Names. 

Once completed, you should configure your DNS records in your DNS Provider, in my case it is Gandi.Net and used the above [Matt Bailey's good guide](https://gist.github.com/matt-bailey/bbbc181d5234c618e4dfe0642ad80297). You have to consider that making these changes and their propagation across DNS and GitHub will take around 24 hours.

How to set up DNS records on gandi.net to use a custom domain on Github Pages

{{< rawhtml >}}
<script src="https://gist.github.com/matt-bailey/bbbc181d5234c618e4dfe0642ad80297.js"></script>
{{</ rawhtml >}}

## Install Ruby on Ubuntu

This step must be executed once in the computer.
First of all, install Ruby.

```sh
$ sudo apt -y install ruby ruby-dev build-essential zlib1g-dev
```

Now, configure Ruby for my Linux's user.

```sh
$ echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
$ echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
$ echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
$ source ~/.bashrc

$ gem install bundler
```

## Install Jekyll with Bundler

This step and next ones must be executed per website or ruby project. In this point your configured custom DNS should be working.
I will download my empty created GitHub Page repository into `~/gitrepos/ghpages-holosec/` directory.

```sh
$ mkdir -p $HOME/gitrepos/ghpages-holosec/; cd $HOME/gitrepos/ghpages-holosec/ 
$ git clone https://github.com/chilcano/ghpages-holosec 
```

__Creating a Jekyll project from scratch__

In this case the `ghpages-holosec` is an empty project, then run next commands.
```sh
$ bundle init
$ bundle add jekyll
```
 
Once Jekyll is installed, we can use it to create the scaffolding for our site.
```sh
$ bundle exec jekyll new --force --skip-bundle .
```

If `ghpages-holosec` is already a Jekyll project, then run next commands:
```sh
// This installs Jekyll and all gems present in Gemfile
$ bundle config set path vendor/bundle

// This installs jekyll and update Gemfile
$ bundle install	
```

## Serving the site for first time

I updated the generated `_config.yml` file with information about `baseurl`, `title`, `email`, etc.
Yes, I'll tweak the `_config.yml` file to apply new design later.
Now, you will see only `Welcome to Jekyll!` sample post.

```sh
$ bundle exec jekyll serve --incremental --watch
```

## Importing a WordPress.com's blog into GitHub Pages site

Go to `https://your-user-name.wordpress.com/wp-admin/export.php` and export your blog's content into a XML, place the xml file in `~/gitrepos/ghpages-holosec/wp_export/`, once completed, execute `jekyll-import` to convert WordPress' XML format into GitHub's MarkDown format.

Install jekyll-import and its dependencies.
```sh
$ bundle add jekyll-import hpricot open_uri_redirections
```

Convert wordpress' blog to Jekyll format.
```sh
$ bundle exec ruby -r rubygems -e 'require "jekyll-import";
    JekyllImport::Importers::WordpressDotCom.run({
      "source" => "wp_export/holisticsecurity.WordPress.2019-11-07.xml",
      "no_fetch_images" => false,
      "assets_folder" => "assets"
    })'
```

## Serving the site again

```sh
$ bundle exec jekyll serve
```

If you are using Google Analytics plugin configured, you can try this:

```sh
$ JEKYLL_ENV=production bundle exec jekyll serve --incremental --watch
```

If you have posts in draft (place your posts in `<site>\_drafts\` folder without `date` and `permalink` in the front-matter.

```sh
$ JEKYLL_ENV=production bundle exec jekyll serve --watch --drafts
```

You will see that all posts were imported.

![Holistic Security About page](/assets/img/2019-10-14-wp-to-github-holosec-1st.png)

## References

- [Bash Script to install Jekyll in Ubuntu](https://github.com/chilcano/how-tos/blob/master/resources/setting_jekyll_in_ubuntu.sh)
- [HolisticSecurity.io - GitHub Pages and Jekyll on Windows 10](https://holisticsecurity.io/2020/03/30/github-pages-and-jekyll-on-windows-10)
- [Installation of Jekyll on Ubuntu](https://jekyllrb.com/docs/installation/ubuntu/)

