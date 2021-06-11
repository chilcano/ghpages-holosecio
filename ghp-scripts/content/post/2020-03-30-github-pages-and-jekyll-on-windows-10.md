---
categories:
- misc
- cms
comments: true
date: "2020-03-30T22:00:00Z"
tags:
- github
- jekyll
- ruby
title: GitHub Pages and Jekyll on Windows 10
url: /2020/03/30/github-pages-and-jekyll-on-windows-10
type: post
layout: single_simple
---
I have a[ Blog hosted on Github Pages created with Jekyll from Linux](https://holisticsecurity.io/2019/10/14/migrating-wordpress-com-blog-to-github-pages-with-jekyll-part1). That [works perfectly and can publish posts frequently](https://holisticsecurity.io/2019/12/10/migrating-wordpress-com-blog-to-github-pages-with-jekyll-part2), but now I would like to do the same but from Windows 10 laptop (older Surface 3 Pro, 4GB RAM, 64GB SSD). The aim of this post is explain you how to prepare and configure Windows 10 to publish post in a new or existing static site created with Jekyll.

To do that I'm going to follow the [Jekyll on Windows](https://jekyllrb.com/docs/installation/windows) guide, basically I'll [download, install and configure a Ruby+Devkit](https://rubyinstaller.org/downloads) version in Windows 10.

[![](/assets/blog20200330/20200330-github-pages-and-jekyll-on-windows-10-1.png)](/assets/blog20200330/20200330-github-pages-and-jekyll-on-windows-10-1.png)

<!--more-->

## Steps

1. Once downloaded and installed Ruby+Devkit, open a CMD as standard user and check the installed version:

```powershell
C:\Users\rmce> ruby --version
ruby 2.6.5p114 (2019-10-01 revision 67812) [x64-mingw32]
```
 
2. Download existing the Github Pages site:

```powershell
C:\Users\rmce> y:
Y:\> cd __gitrepos
Y:\__gitrepos> git clone https://github.com/chilcano/ghpages-holosec
Y:\__gitrepos> cd ghpages-holosec
```

3. Install Bundler:
```powershell
Y:\__gitrepos\ghpages-holosec> gem install bundler
Y:\__gitrepos\ghpages-holosec> bundle config set path 'vendor/bundle'
```

4. Install Jekyll and all Gems via Bundler:

```powershell
Y:\__gitrepos\ghpages-holosec> bundle 
```

5. Check if Jekyll was installed properly:

```powershell
Y:\__gitrepos\ghpages-holosec> bundle exec jekyll -v
jekyll 4.0.0
```

6. Now we are ready to serve the site in our computer:

```powershell
Y:\__gitrepos\ghpages-holosec> bundle exec jekyll serve
```

7. If you are using Google Analytics plugin configured, you can try this:

```powershell
Y:\__gitrepos\ghpages-holosec> set JEKYLL_ENV=production 
Y:\__gitrepos\ghpages-holosec> bundle exec jekyll serve --incremental --watch 
Configuration file: Y:/__gitrepos/ghpages-holosec/_config.yml
            Source: Y:/__gitrepos/ghpages-holosec
       Destination: Y:/__gitrepos/ghpages-holosec/_site
 Incremental build: enabled
      Generating...
       Jekyll Feed: Generating feed for posts
                    done in 192.797 seconds.
 Auto-regeneration: enabled for 'Y:/__gitrepos/ghpages-holosec'
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.
```

Or instead of CMD using PowerShell Terminal.
```PowerShell
Y:\__gitrepos\ghpages-holosec>
$> Set-Variable -name JEKYLL_ENV -value production; bundle exec jekyll serve --incremental --watch
```

And if you have posts in draft, run this. Only be aware to place your posts in `<site>\_drafts\` folder without `date` and `permalink` in the front-matter.
```PowerShell
$> Set-Variable -name JEKYLL_ENV -value production; bundle exec jekyll serve --watch --drafts
```

[![](/assets/blog20200330/20200330-github-pages-and-jekyll-on-windows-10-2.png)](/assets/blog20200330/20200330-github-pages-and-jekyll-on-windows-10-2.png)