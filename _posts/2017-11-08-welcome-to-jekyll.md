---
layout: post
title: Jekyll_搭建简易博客
date: 2017-11-08
tags: 博客
---

### Jekyll
简介


安装 jekyll

```
$ gem install jekyll
```

创建

```
$ jekyll new bamboogBlog
```

进入博客目录

```
$ cd XXX/bamboogBlog
```

启动服务

```
$ jekyll serve
```

在浏览器里输入： [http://localhost:4000](http://localhost:4000)，看效果。



- 问题1
  -
```
bamboogBlog jekyll  serve
/usr/lib/ruby/2.3.0/rubygems/core_ext/kernel_require.rb:55:in `require': cannot load such file -- bundler (LoadError)
 from /usr/lib/ruby/2.3.0/rubygems/core_ext/kernel_require.rb:55:in `require'
 from /var/lib/gems/2.3.0/gems/jekyll-3.6.2/lib/jekyll/plugin_manager.rb:48:in `require_from_bundler'
 from /var/lib/gems/2.3.0/gems/jekyll-3.6.2/exe/jekyll:11:in `<top (required)>'
 from /usr/local/bin/jekyll:23:in `load'
 from /usr/local/bin/jekyll:23:in `<main>'
```
  - ans

   ```
   apt-get install bundler

   ```

- 问题2(类似)
    ```
    bamboogBlog jekyll  serve
/var/lib/gems/2.3.0/gems/bundler-1.16.0/lib/bundler/resolver.rb:288:in `block in verify_gemfile_dependencies_are_found!': Could not find gem 'minima (~> 2.0)' in any of the gem sources listed in your Gemfile. (Bundler::GemNotFound)
 from /var/lib/gems/2.3.0/gems/bundler-1.16.0/lib/bundler/resolver.rb:256:in `each'
 from /var/lib/gems/2.3.0/gems/bundler-1.16.0/lib/bundler/resolver.rb:256:in `verify_gemfile_dependencies_are_found!'
 from /var/lib/gems/2.3.0/gems/bundler-1.16.0/lib/bundler/resolver.rb:48:in `start'
 from /var/lib/gems/2.3.0/gems/bundler-1.16.0/lib/bundler/resolver.rb:22:in `resolve'
 from /var/lib/gems/2.3.0/gems/bundler-1.16.0/lib/bundler/definition.rb:257:in `resolve'
 from /var/lib/gems/2.3.0/gems/bundler-1.16.0/lib/bundler/definition.rb:170:in `specs'
 from /var/lib/gems/2.3.0/gems/bundler-1.16.0/lib/bundler/definition.rb:237:in `specs_for'
 from /var/lib/gems/2.3.0/gems/bundler-1.16.0/lib/bundler/definition.rb:226:in `requested_specs'
 from /var/lib/gems/2.3.0/gems/bundler-1.16.0/lib/bundler/runtime.rb:108:in `block in definition_method'
 from /var/lib/gems/2.3.0/gems/bundler-1.16.0/lib/bundler/runtime.rb:20:in `setup'
 from /var/lib/gems/2.3.0/gems/bundler-1.16.0/lib/bundler.rb:107:in `setup'
 from /var/lib/gems/2.3.0/gems/jekyll-3.6.2/lib/jekyll/plugin_manager.rb:50:in `require_from_bundler'
 from /var/lib/gems/2.3.0/gems/jekyll-3.6.2/exe/jekyll:11:in `<top (required)>'
 from /usr/local/bin/jekyll:23:in `load'
 from /usr/local/bin/jekyll:23:in `<main>'

    ```
  - ans
    ```
    gem install minima
    ```

- 上传github
  - 申请账号
  - 添加类似这样的仓库:`bamboog.github.io` ; `bamboog`是你对应的github名字
  - push jekyll 生成的blog项目到github,类似这样访问:https://bamboog.github.io/
  - 完事
- 修改
