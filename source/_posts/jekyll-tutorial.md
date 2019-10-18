---
title: Jekyll教程->>滑稽预警
author: Raptazure
tags:
	感悟
---

​                                                                                                     *— Notes by Raptazure*

### Installation(Linux)

- 需要安装ruby以及gems

- 通过gem安装jekyll以及bundler `gem install jekyll bundler`

- 注意PATH配置(以Manjaro为例) 

   `export PATH=“$PATH:/home/username/.gem/ruby/2.6.0/bin"`
   
- 通过jekyll -v命令查看是否安装成功

<!-- more -->

### Creating a Site

- `jekyll hello_world`

- `cd hello_world/`

- `bundle exec jekyll serve`

- try to visit http://127.0.0.1:4000/

- blog posts that you wirte go inside of   ->  _posts 

  final output of your website  ->  _site

  _config.yml  ->  settings for your Jekyll website

  Gemfile  ->  store all of the dependencied for our website

### Front Matter

- It contains certain information about those pages or it might contain something like a title or the date the page was written or the author of the page. Front matter can be wrritten in YAML and JSON.
- Like Variables?
- Open “welcome-to-jekyll.markdown” to see its format. (Typora)

### Writing Posts

- Pay attention to the name, e.g    2019-10-13-jekyll-tutorial.md  works.
- Add your own front matter.
- The font matter (such as the date) plays a role in the URL of the page
- You can also create sub-directories to organize your posts.

### Working with Drafts

- Create a new folder named _drafts in `hello_world` 
- Create your drafts `my-first-draft.md` and they are not going to show up in your site.
- run `jekyll serve –draft` to show your drafts in the site. And it’s given the date it was last modified.

### Creating Pages

- About me Page(about.md) ,  Donate me Page(donate.md) 

  Create them and use `localhost:4000/donate` or `http://127.0.0.1:4000/about/` to visit.
  

### Permalinks

- Compare the link and the _site folder structure

  `http://127.0.0.1:4000/jekyll/update/2019/10/12/welcome-to-jekyll.html`  and
  `/home/username/hello_world/_site/jekyll/update/2019/10/12/`
  
- How to change the category and the date  without changing the URL?

  ->  Define a permanent link for this page

     e.g. In the front matter, add a line:  permalink: “/my-new-url/test” 

  ​           if you want to use the category, add: permalink: /:categories

  ​           another example:  permalink: /:categories/:year/:month/:title

  ​            (put whatever you want! even .html .php)

- Create a custom unique permalink for each of the blog posts and each of the pages on your site.

### Front Matter Defaults

- Go to _config.yml, add something at the bottom:

  ```yaml
  defaults:
  -
      scope:
        path:""
	      type:"post"
      values:
        layout:"post"
	```
- Remember to reload the bundle

### Themes

- Come to https://rubugems.org
- search for jekyll-theme
- open Gemfile and add `gem "jekyll-theme-architect"`
- go to the terminal and type`bundle install`
- _config.yml  `theme: jekyll-theme-architect`
- Restart the server `bundle exec jekyll serve`

### Finally

- Go to the terminal and run `gem uninstall jekyll bundler`
- Pardon???

### 后续…

​	上面看似是一个非常正经的教程(感谢Giraffe Academy), 然而当窝用jekyll部署网站的时候似乎遇到了一些困难(对git的了解还需要深入鸭), 再加上对Hexo特性的偶然了解, 让窝决定转移战线了…

​	折腾jekyll的时间也不算很短, 最后却弃坑了…看似浪费了很多时间, 然而因为在这个过程中有了一些对YAML的基本了解, 以及jekyll和hexo的组织逻辑比较相似, 所以总体还是蛮有收获的…毕竟不去尝试也不容易取得进展啊。

​	需要学的知识还有很多很多，而这只是一个开始，向着远方加油吧。

