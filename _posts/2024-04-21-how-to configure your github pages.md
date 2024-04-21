---
title: How to configure your github pages
description: >-
  Get started with Chirpy basics in this comprehensive overview.
  You will learn how to install, configure, and use your first Chirpy-based website, as well as deploy it to a web server.
author: upthen
date: 2024-04-21 22:00:00 +0800
categories: [Blogging, Tutorial]
tags: [github pages]
pin: true
media_subpath: '/posts/20240421'
---

一直想给自己整个博客站点，之前用 GitHub Pages 弄过一次，但是那时候刚入行，英文文档啥的都读不懂，git 也不会用，就搁置了，一搁置就是好几年，最近想起来这茬，就花了一些时间弄了一下，本文是整理的相关记录。

> TL,DR: 兜兜转转一圈后，发现直接 fork 社区现成模板改改就能用，所以，直接跳到第三章吧。
{: .prompt-tip }

## 1. 创建GitHub Pages 仓库，进行相关配置

[Quickstart for GitHub Pages - GitHub Docs](https://docs.github.com/en/pages/quickstart)

## 2. 丰富 Github Pages

[Adding content to your GitHub Pages site using Jekyll - GitHub Docs](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/adding-content-to-your-github-pages-site-using-jekyll#about-content-in-jekyll-sites)

要创建一个完整的博客站点，需要使用到 Jekyll 这个ruby 包。

使用 Jekll 之前，必须先创建一个 `Jekyll` 站点。

### 2.1 使用 Jekyll 创建 GitHub pages 站点

[Creating a GitHub Pages site with Jekyll - GitHub Docs](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll)

在使用 `Jekyll` 之前，必须安装 `Jekyll`  和 `Git`.

#### 2.1.1 `Jekyll` 环境安装配置

[Installation | Jekyll • Simple, blog-aware, static sites (jekyllrb.com)](https://jekyllrb.com/docs/installation/)

##### 1. 安装 `Jekyll` 的环境要求

> Jekyll is a [Ruby Gem](https://jekyllrb.com/docs/ruby-101/#gems) that can be installed on most systems.

- Ruby > 2.5.0，使用 `ruby -v` 查看版本
- RubyGems (check your Gems version using `gem -v`))
- [GCC](https://gcc.gnu.org/install/) and [Make](https://www.gnu.org/software/make/) (check versions using `gcc -v`,`g++ -v`, and `make -v`)

##### 2. 安装指导

- [macOS](https://jekyllrb.com/docs/installation/macos/)
- [windows](https://jekyllrb.com/docs/installation/windows/)

##### 3. Jekyll on macOS

支持的 macOS 版本：

- Ventura (macOS 13)
- Monterey (macOS 12)
- Big Sur (macOS 11)



##### 4. macOS如何安装 Ruby

**gem 是什么？** 

在 macOS 上，gem 是 Ruby 的包管理器，用于安装、管理和发布 Ruby 应用程序和库。gem 允许用户轻松地安装第三方 Ruby 应用程序和库，并管理它们的版本。（类似 node npm的关系）

macOS 自带 ruby ，但是不建议使用系统默认安装的 ruby 版本，相关原因见这篇文章：

👉[why you shouldn’t use the system Ruby](https://www.moncefbelyamani.com/why-you-shouldn-t-use-the-system-ruby-to-install-gems-on-a-mac/)

应该使用 [asdf](https://asdf-vm.com/), [chruby](https://github.com/postmodern/chruby), [rbenv](https://github.com/rbenv/rbenv), or [rvm](https://rvm.io/) 等版本管理工具安装单独的新一些的版本的ruby。版本管理工具允许轻松的安装和切换多个版本的 ruby。

推荐使用 `chruby`, 它最简单，然后出问题的可能性最小。

**如何安装和配置 ruby？**

- 安装 `Homebrew`

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

![截屏2024-04-14 14.53.23](https://cherish-1256678432.cos.ap-nanjing.myqcloud.com/typora/%E6%88%AA%E5%B1%8F2024-04-14%2014.53.23.png)

- 安装 chruby 和 ruby-install

```bash
brew install chruby ruby-install xz
```

![截屏2024-04-14 14.54.43](https://cherish-1256678432.cos.ap-nanjing.myqcloud.com/typora/%E6%88%AA%E5%B1%8F2024-04-14%2014.54.43.png)

- 安装最新版 ruby

  ```bash
  ruby-install ruby 3.1.3
  ```

  

  ![截屏2024-04-14 15.01.05](https://cherish-1256678432.cos.ap-nanjing.myqcloud.com/typora/%E6%88%AA%E5%B1%8F2024-04-14%2015.01.05-20240414150451217.png)

- 配置 `shell` 自动使用 `chruby`

  ```bash
  echo "source $(brew --prefix)/opt/chruby/share/chruby/chruby.sh" >> ~/.zshrc
  echo "source $(brew --prefix)/opt/chruby/share/chruby/auto.sh" >> ~/.zshrc
  echo "chruby ruby-3.1.3" >> ~/.zshrc # run 'chruby' to see actual version
  ```

​		如果你使用的终端还是 bash, 将 `.zshrc` 替换为  `.bash_profile`。

​		$(brew --prefix) 表示的是安装 homebrew 的目录，需要替换为实际地址，如：

```bash
echo "source /opt/homebrew/opt/chruby/share/chruby/chruby.sh" >> ~/.zshrc
echo "source /opt/homebrew/opt/chruby/share/chruby/auto.sh" >> ~/.zshrc
echo "chruby ruby-3.1.3" >> ~/.zshrc # run 'chruby' to see actual version
```

- 配置好后测试一下

  ```bash
  chruby
  ```

![截屏2024-04-14 15.29.47](https://cherish-1256678432.cos.ap-nanjing.myqcloud.com/typora/%E6%88%AA%E5%B1%8F2024-04-14%2015.29.47.png)

​	(3) 如何使用 chruby 切换 ruby 版本

```bash
chruby 3.1.2
```

切换到 3.1.2

![截屏2024-04-14 15.31.24](https://cherish-1256678432.cos.ap-nanjing.myqcloud.com/typora/%E6%88%AA%E5%B1%8F2024-04-14%2015.31.24.png)

##### 5. macOS 安装 Jekyll

安装好 ruby 之后，就可以安装最新的 Jekyll gem 了。

```bash
gem install jekyll
```

![截屏2024-04-14 15.35.56](https://cherish-1256678432.cos.ap-nanjing.myqcloud.com/typora/%E6%88%AA%E5%B1%8F2024-04-14%2015.35.56.png)



#### 2.1.2 使用 Bundler 运行 Jekyll

**Bundler 安装**：　👉[Bundler](https://bundler.io/)	

```bash
gem install bundler
```

![截屏2024-04-14 15.55.37](https://cherish-1256678432.cos.ap-nanjing.myqcloud.com/typora/%E6%88%AA%E5%B1%8F2024-04-14%2015.55.37.png)

#### 2.1.3 为你的站点创建一个仓库

见第一章

#### 2.1.4 创建你的站点

1. 将第一章中创建的仓库克隆到本地

2. 在仓库中新建 `docs` 目录，进入该目录，运行如下 Jekyll 命令，初始化一个 Jekyll site.

   ```bash
   // 仓库目录 upthen.github.io
   mkdir docs
   
   cd docs
   
   jekyll new --skip-bundle . #Creates a Jekyll site in the current directory
   ```

3. 打开 Gemfile 文件，注释掉以 `gem "jekyll" ` 开头的行，将以 `# gem "github-pages"` 开头的行解除注释，并将其修改为：

   ```bash
   gem "github-pages", "~> GITHUB-PAGES-VERSION", group: :jekyll_plugins
   ```

   将 GITHUB-PAGES-VERSION 替换为最新版的 ``github-pages` gem` , 在这里可以找到最新版：👀[Dependency versions](https://pages.github.com/versions/).

   根据下图，目前最新版是 231.

   ```bash
   gem "github-pages", "~> 231", group: :jekyll_plugins
   ```

   设置完成后，关闭 Gemfile 文件。修改完的配置如下：

   ![image-20240414170732518](https://cherish-1256678432.cos.ap-nanjing.myqcloud.com/typora/image-20240414170732518.png)

   

   ```bash
   source "https://rubygems.org"
   # Hello! This is where you manage which Jekyll version is used to run.
   # When you want to use a different version, change it below, save the
   # file and run `bundle install`. Run Jekyll with `bundle exec`, like so:
   #
   #     bundle exec jekyll serve
   #
   # This will help ensure the proper Jekyll version is running.
   # Happy Jekylling!
   #gem "jekyll", "~> 4.3.3" # 注释掉这一行
   # This is the default theme for new Jekyll sites. You may change this to anything you like.
   gem "minima", "~> 2.5"
   # If you want to use GitHub Pages, remove the "gem "jekyll"" above and
   # uncomment the line below. To upgrade, run `bundle update github-pages`.
   gem "github-pages", "~> 231", group: :jekyll_plugins # 这一行解除注释,并修改
   # If you have any plugins, put them here!
   group :jekyll_plugins do
     gem "jekyll-feed", "~> 0.12"
   end
   
   # Windows and JRuby does not include zoneinfo files, so bundle the tzinfo-data gem
   # and associated library.
   platforms :mingw, :x64_mingw, :mswin, :jruby do
     gem "tzinfo", ">= 1", "< 3"
     gem "tzinfo-data"
   end
   
   # Performance-booster for watching directories on Windows
   gem "wdm", "~> 0.1.1", :platforms => [:mingw, :x64_mingw, :mswin]
   
   # Lock `http_parser.rb` gem to `v0.6.x` on JRuby builds since newer versions of the gem
   # do not have a Java counterpart.
   gem "http_parser.rb", "~> 0.6.0", :platforms => [:jruby]
   
   ```

4. 在命令行中运行 `bundle install` .

   ```bash
   # /upthen.github.io/docs
   bundle install
   ```

5. 当仓库位于子目录时，按如下要求修改 _config.yml（暂时没弄，没看出有啥需要修改的）

   ```bash
   domain: upthen.github.io       # if you want to force HTTPS, specify the domain without the http at the start, e.g. example.com
   url: https://upthen.github.io  # the base hostname and protocol for your site, e.g. http://example.com
   baseurl: /REPOSITORY-NAME/      # place folder name if the site is served in a subfolder
   ```

6. 本地测试

   👀[Testing your GitHub Pages site locally with Jekyll](https://docs.github.com/en/articles/testing-your-github-pages-site-locally-with-jekyll)

   - 安装 `webrick`

     Ruby 3.0 以上不在默认安装 `webrick`, 所以需要先装一下，不然下一步执行 `bundle exec` 时会报错；

     ```bash
     bundle add webrick
     ```

     

   - 在目录中运行如下命令：`bundle exec Jekyll serve`

     ```bash
     bundle exec jekyll serve
     ```

     启动后，服务默认运行在 `http://localhost:4000/` 这个地址。

![image-20240414172946998](https://cherish-1256678432.cos.ap-nanjing.myqcloud.com/typora/image-20240414172946998.png)

![image-20240414173028085](https://cherish-1256678432.cos.ap-nanjing.myqcloud.com/typora/image-20240414173028085.png)

7. 将更改推送到github

8. 预览

   ![image-20240414183438163](https://cherish-1256678432.cos.ap-nanjing.myqcloud.com/typora/image-20240414183438163.png)

成功了。

## 3. 直接从社区白嫖一套模板

在 这里可以找到很多模板：🐬[Themes | Jekyll • Simple, blog-aware, static sites (jekyllrb.com)](https://jekyllrb.com/docs/themes/)

直接点到 👉[jekyll-theme · GitHub Topics](https://github.com/topics/jekyll-theme)， 这里有一个 star 最多的模板排行，直接选一个大佬做好的仓库，fork 到自己的 GitHub，然后克隆下来使用。

这里我选择这个模板，不愧是 6.2k star 的项目，人家这个教程写的很详细，还提供了模板直接供使用。

![image-20240421203529518](https://cherish-1256678432.cos.ap-nanjing.myqcloud.com/typora/image-20240421203529518.png)

🦊[cotes2020/jekyll-theme-chirpy: A minimal, responsive, and feature-rich Jekyll theme for technical writing. (github.com)](https://github.com/cotes2020/jekyll-theme-chirpy)

图中的 Getting Started 就是使用文档，可以在这个仓库找到这个 Live Demo ，点击预览，可以访问图中这个站点，查看这篇教程。

这里有2种方式使用，一个是用作者提供的模板创建自己的 GitHub Pages 仓库，另一个则是直接 fork 这个模板到自己的仓库，然后改成自己的 `USERNAME.github.io` .

然后就是把一些配置改成自己的站点配置了。

如果想要在本地运行的话，按照 第2节中的操作配置好本地环境后，就可以运行了，方法也是一样。

- `bundle install`  安装依赖
- `bundle exec jekyll serve` 运行服务

然后就是使用 GitHub 发布这块了，这块主要注意一下，发布源要选 GitHub Actions。默认不是这个，默认是

![image-20240421204755225](https://cherish-1256678432.cos.ap-nanjing.myqcloud.com/typora/image-20240421204755225.png)

默认选项是 Deploy from a branch. 我第一遍没仔细看文档，这里配错了，然后访问的时候一直是空白页面。

## 附录：

### Ruby 包管理工具：gem

在 macOS 上，gem 是 Ruby 的包管理器，用于安装、管理和发布 Ruby 应用程序和库。gem 允许用户轻松地安装第三方 Ruby 应用程序和库，并管理它们的版本。要在 macOS 上使用 gem，可以按照以下步骤进行：

1. **安装 gem**：

   - gem 通常随 Ruby 一起安装。如果您已经安装了 Ruby，则 gem 也应该已经可用。您可以通过以下命令验证 gem 的安装：

     ```bash
     gem --version
     ```

2. **使用 gem**：

   - 安装 gem 包：要安装特定的 gem 包，可以使用以下命令：

     ```bash
     gem install <gem_name>
     ```

   - 列出已安装的 gem 包：您可以使用以下命令列出已安装的 gem 包：

     ```bash
     gem list
     ```

   - 卸载 gem 包：如果需要卸载某个 gem 包，可以使用以下命令：

     ```bash
     gem uninstall <gem_name>
     ```

3. **其他常用操作**：

   - 更新 gem：您可以使用以下命令更新 gem 自身到最新版本：

     ```bash
     gem update --system
     ```

   - 搜索 gem 包：如果您需要搜索特定的 gem 包，可以使用以下命令：

     ```bash
     gem search <keyword>
     ```

通过 gem，您可以方便地管理 Ruby 应用程序和库，以及它们的依赖关系。记得在使用 gem 时，最好使用合适的权限，以避免权限问题导致的安全隐患。

### macOS 包管理工具：Homebrew

Homebrew 是 macOS 上一款流行的包管理器（Package Manager），用于简化软件包的安装和管理过程。通过 Homebrew，用户可以方便地安装各种软件包、工具和库，而无需手动下载和编译源代码。

一些 Homebrew 的特点包括：

- 提供简单的命令行界面，使用户可以轻松地搜索、安装、更新和卸载软件包。
- 自动解决软件包之间的依赖关系，确保安装的软件包能够正常运行。
- 提供一个庞大的软件包仓库，涵盖了各种常用的开源软件和工具。
- 允许用户自定义安装路径，避免与系统自带软件包冲突。

通过 Homebrew，用户可以快速、方便地在 macOS 系统上安装各种软件包，使得软件的管理和维护变得更加简单和高效。
