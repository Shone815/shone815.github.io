Shone815 Blog User Manual
====================

* Basics
	* [Getting Started](#getting-started)
	* [Development](#development)
	* [Config](#configs)
	* [Posts](#posts)
* Components
	* [SideBar](#sidebar)
	* [Mini About Me](#mini-about-me)
	* [Featured Tags](#featured-tags)
	* [Keynote Layout](#keynote-layout)
* Misc
	* [Comment](#comment)
	* [Analytics](#analytics)
	* [SEO Title](#seo-title)
* [FAQ](#faq)
* [Releases](#releases) 


### Getting Started

1. You will need [Ruby](https://www.ruby-lang.org/en/) and [Bundler](https://bundler.io/) to use [Jekyll](https://jekyllrb.com/). Following [Using Jekyll with Bundler](https://jekyllrb.com/tutorials/using-jekyll-with-bundler/) to fullfill the enviromental requirement.

2. Installed dependencies in the `Gemfile`:

```sh
$ bundle install 
```

3. Serve the website (`localhost:4000` by default):

```sh
$ bundle exec jekyll serve  # alternatively, npm start
```

### Development

To modify the theme, you will need [Grunt](https://gruntjs.com/). There are numbers of tasks you can find in the `Gruntfile.js`, includes minifing JavaScript, compiling `.less` to `.css`, adding banners to keep the Apache 2.0 license intact, watching for changes, etc. 

Yes, they were inherited and are extremely old-fashioned. There is no modularization and transpilation, etc.

Critical Jekyll-related code are located in `_include/` and `_layouts/`. Most of them are [Liquid](https://github.com/Shopify/liquid/wiki) templates.

This theme uses the default code syntax highlighter of jekyll, [Rouge](http://rouge.jneen.net/), which is compatible with Pygments theme so just pick any pygments theme css (e.g. from [here](http://jwarby.github.io/jekyll-pygments-themes/languages/javascript.html) and replace the content of `highlight.less`.


### Configs

You can easily customize the blog by modifying `_config.yml`:

```yml
# Site settings
title: Shone815 Blog             # title of your website
SEOTitle: Shone815 Blog          # check out docs for more detail
description: "Cool Blog"    # ...

# SNS settings      
github_username: Shone815     # modify this account to yours
weibo_username: Shone815      # the footer woule be auto-updated.

# Build settings
paginate: 10                # nums of posts in one page
```

For more options, please check out [Jekyll - Official Site](http://jekyllrb.com/). 
Most of them are very descriptive so feel brave to dive into code directly as well. 


### Posts

Posts are simply just Markdown files in the `_posts/`. 
Metadata of posts are listed in a YAML style _front-matter_.

For instance, [Hello 2015])(https://shone815.github.io/2015/01/29/hello-2015/) has the front-matter of this:

```yml
---
layout:     post
title:      "Hello 2015"
subtitle:   " \"Hello World, Hello Blog\""
date:       2024-05-30 12:00:00
author:     "Shone815"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Life
    - Meta
---
```

> Note: `tags` section can also be written as `tags: [Life, Meta]`.

After [Rake](https://github.com/ruby/rake) is introduced, we can use the command below to simplify the post creation:

```
rake post title="Hello 2015" subtitle="Hello World, Hello Blog"
```

This command will automatially generate a sample post similar as above under the `_posts/` folder.

There are a bunch of _advanced_ configs:

1. a _text style_ header like [this](https://shone815.github.io/2019/09/08/spacemacs-workflow/) with

```yml
header-style: text 
```

2. Turning on Latex support:

```yml
mathjax: true
```

3. Adding a mask to the header picture:

```yml
header-mask: 0.3
```

Etc.


### SideBar

![](http://shone815.github.io/img/blog-sidebar.jpg)

**SideBar** provides possible modules to show off more personal information.

```yml
# Sidebar settings
sidebar: true   # default true
sidebar-about-description: "your description here"
sidebar-avatar: /img/avatar-shone815.jpg     # use absolute URL.
```

Modules *[Featured Tags](#featured-tags)*, *[Mini About Me](#mini-about-me)* and are turned on by default and you can add your own. The sidebar is naturally responsive, i.e. be pushed to bottom in a smaller screen (`<= 992px`, according to [Bootstarp Grid System](http://getbootstrap.com/css/#grid))  


### Mini About Me

**Mini-About-Me** displays your avatar, description and all SNS buttons if  `sidebar-avatar` and `sidebar-about-description` variables are set. 

It would be hidden in a smaller screen when the entire sidebar are pushed to bottom. Since there is already SNS portion there in the footer.

### Featured Tags

**Featured-Tags** is similar to any cool tag features in website like [Medium](http://medium.com).
Started from V1.4, this module can be used even when sidebar is off and displayed always in the bottom. 

```yml
# Featured Tags
featured-tags: true  
featured-condition-size: 1     # A tag will be featured if the size of it is more than this condition value
```

The only thing need to be paid attention to is `featured-condition-size`, which indicate a criteria that tags need to have to be able to "featured". Internally, a condition `{% if tag[1].size > {{site.featured-condition-size}} %}` are made.


### Keynote Layout

![](http://shone815.github.io/img/blog-keynote.jpg)

There is a increased trend to use Open Web technology for keynotes and presentations via Reveal.js, Impress.js, Slides, Prezi etc. I consider a modern blog should have first-class support to embed these HTML based presentation so **Keynote layout** are made.

To use, in the **front-matter**:

```yml
---
layout:     keynote
iframe:     "http://shone815.github.io/js-module-7day/"
---
```

The `iframe` element will be automatically resized to adapt different form factors and device orientation. 
Because most of the keynote framework prevent the browser default scroll behavior. A bottom-padding is set to help user and imply user that more content could be presented below.


### Comment

> Help Wanted: Moving to a Github-based solution.

Currently, [Disqus](http://disqus.com) <del> and [Duoshuo](http://duoshuo.com)</del> are supported as third party discussion system.

Second, from V1.5, you can easily complete your comment configuration by just adding your **short name** into `_config.yml`:


```yml
# Baidu Analytics
ba_track_id: 4cc1f2d8f3067386cc5cdb626a202900

Just checkout the code offered by Google/Baidu, and copy paste here, all the rest is already done for you.

(Google might ask for meta tag `google-site-verification`)


### SEO Title

Before V1.4, site setting `title` is not only used for displayed in Home Page and Navbar, but also used to generate the `<title>` in HTML.
It's possible that you want the two things different. For me, my site-title is **Shone815 Blog”** but I want the title shows in search engine is **“Shone815的博客 | Shone815 Blog”** which is multi-language.

So, the SEO Title is introduced to solve this problem, you can set `SEOTitle` different from `title`, and it would be only used to generate HTML `<title>` and setting DuoShuo Sharing.
