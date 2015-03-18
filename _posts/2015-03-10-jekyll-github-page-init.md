---
layout: post
title: "Jekyll与Github-page的安装"
tags: github config tutorial
---

前一篇文章[《Github 初步配置》]({% post_url 2015-03-09-github-config %})里记录了一下Github配置过程。  
接下来继续说一下博客程序jekyll和github-page工具的安装(还是以mac为例)。

### 一、安装Jekyll
细节请参考各个官方链接：  
[http://jekyllrb.com/docs/installation/](http://jekyllrb.com/docs/installation/)  
[https://github.com/jekyll/jekyll](https://github.com/jekyll/jekyll)  
[https://help.github.com/articles/using-jekyll-with-pages/](https://help.github.com/articles/using-jekyll-with-pages/)  

#### 1.安装ruby和gem：如果是OSX，已经自带了，无需安装

#### 2.有幸生活在大陆的童鞋们，有可能需要用淘宝的源替代官方源
		{% highlight sh %}
gem sources -r https://rubygems.org/
gem sources -a http://ruby.taobao.org/
gem sources # 确认一下设置后的最终结果
		{% endhighlight %}
#### 3.不(qiang)放(po)心(zheng)的话可以先升级一下gem
        {% highlight sh %}
          sudo gem update --system
        {% endhighlight %}
#### 4.安装jekyll
		{% highlight sh %}
          gem install jekyll
		{% endhighlight %}
#### 5.安装pygments（代码高亮）
        {% highlight sh %}
          sudo gem install pygments.rb
        {% endhighlight %}
#### 6.创建博客目录
        {% highlight sh %}
          jekyll new myblog # 假设创建到~/myblog目录下
        {% endhighlight %}
#### 7.如果哪天又发作了，想要手工升级jekyll
        {% highlight sh %}
          gem update jekyll
        {% endhighlight %}

### 二、与github-pages的集成

#### 1.安装Bundler
        {% highlight sh %}
          gem install bundler
        {% endhighlight %}
#### 2.项目目录下建立文件Gemfile，加入以下内容
	{% highlight ruby %}
source 'https://rubygems.org/'
require 'json'
require 'open-uri'
versions = JSON.parse(open('https://pages.github.com/versions.json').read)
gem 'github-pages', versions['github-pages']
	{% endhighlight %}
这样在启动时会自动与github服务器对比各个依赖的版本号，以确保本地build结果会与github服务器build结果一致（这里假设你上传的是源文件而不是build结果——这种方式缺点是不能使用插件）。  
一样的，大陆用户可能需要把官方源替换为淘宝源。

#### 3.把Gemfile.lock这货排除出版本控制
        {% highlight sh %}
		echo "Gemfile.lock" >> ~/myblog/.gitignore
        {% endhighlight %}
#### 4.使用bundler安装github-pages相关的依赖
        {% highlight sh %}
		sudo bundle install
        {% endhighlight %}
#### 5.使用bundler启动jekyll服务（jekyll会自动watch目录变化并自动rebuild）
        {% highlight sh %}
		bundle exec jekyll serve # 然后就可以访问 http://127.0.0.1:4000/
        {% endhighlight %}
#### 6.必要时手动更新bundler
        {% highlight sh %}
		sudo bundle update
        {% endhighlight %}

然后就可以开始写博客啦，详情将在下一篇文章里讲。  

### 三、部署博客到github

#### 1.在github上创建一个repository  
这里假设使用user page的方式（如果不知道其它方式，那就用这个没错）。  
建立的repository名字为：watchzerg.github.io （把其中的watchzerg换成自己的github用户名，下同）

#### 2.把本地的项目推到github上刚才建立的repository上
        {% highlight sh %}
cd myblog
git init # 初始化当前目录供git管理
touch README.md # 创建描述文件供github展示
git add . # 当前目录和子目录加入git stage（jekyll自动排除了构建好的_site目录）
git commit -m "big bang" # 从stage提交到master分支
git remote add origin https://github.com/watchzerg/watchzerg.github.io.git # 关联到远程（记得替换用户名）
git push -u origin master # 数据真正push到github上
        {% endhighlight %}










