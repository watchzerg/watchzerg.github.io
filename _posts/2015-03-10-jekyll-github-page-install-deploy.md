---
layout: post
title: "博客搭建(二) Jekyll与Github-page的安装和部署"
tags: github config tutorial
---
### 一、安装ruby和bundler
更多细节请参考各个官方链接：  
[http://jekyllrb.com/docs/installation/](http://jekyllrb.com/docs/installation/)  
[https://github.com/jekyll/jekyll](https://github.com/jekyll/jekyll)  
[https://help.github.com/articles/using-jekyll-with-pages/](https://help.github.com/articles/using-jekyll-with-pages/)  

#### 1.(可选)安装ruby和gem：如果是OSX，已经自带了，无需安装
		{% highlight sh %}
brew install ruby # 未来升级可以用 brew upgrade ruby
		{% endhighlight %}
可以按提示替换系统自带ruby（有一定风险）；或者安装ruby的版本管理工具rvm之类
#### 2.有幸生活在大陆的童鞋们，有可能需要替换一下官方源
		{% highlight sh %}
gem sources -a https://gems.ruby-china.org/ -r https://rubygems.org/
gem sources -l # 确认一下设置后的最终结果
# 未来升级可以用 gem update --system
		{% endhighlight %}

#### 3.安装bundler
	{% highlight sh %}
gem install bundler # 未来升级可以用 gem update bundler
	{% endhighlight %}

#### 4.配置bundler镜像
	{% highlight sh %}
bundle config mirror.https://rubygems.org https://gems.ruby-china.org
	{% endhighlight %}

### 二、本地安装和部署Jekyll
更多细节请参考各个官方链接：  
[http://jekyllrb.com/docs/installation/](http://jekyllrb.com/docs/installation/)  
[https://github.com/jekyll/jekyll](https://github.com/jekyll/jekyll)  
[https://help.github.com/articles/using-jekyll-with-pages/](https://help.github.com/articles/using-jekyll-with-pages/)

#### 1.安装jekyll
		{% highlight sh %}
gem install jekyll # 未来升级可以用 gem update jekyll
		{% endhighlight %}
#### 2.安装pygments（代码高亮）
        {% highlight sh %}
gem install pygments.rb # 未来升级可以用 gem update pygments.rb
        {% endhighlight %}
#### 3.创建博客目录
        {% highlight sh %}
# 假设创建到~/myblog目录下				
cd ~
jekyll new myblog
        {% endhighlight %}

### 三、与github-pages的集成

#### 1.项目目录下建立文件Gemfile，加入以下内容
	{% highlight ruby %}
source 'https://gems.ruby-china.org/'
require 'json'
require 'open-uri'
versions = JSON.parse(open('https://pages.github.com/versions.json').read)
gem 'github-pages', versions['github-pages']
	{% endhighlight %}
这样在启动时会自动与github服务器对比各个依赖的版本号，以确保本地build结果会与github服务器build结果一致（这里假设你上传的是源文件而不是build结果——后者的缺点是不能使用插件）。  
一样的，大陆用户可能需要把官方源替换为淘宝源。

#### 2.把Gemfile.lock这货排除出版本控制
        {% highlight sh %}
echo "Gemfile.lock" >> ~/myblog/.gitignore
        {% endhighlight %}
#### 3.使用bundler安装github-pages相关的依赖
        {% highlight sh %}
# 需要继续在~/myBlog目录下，也就是含有Gemfile的目录下执行
bundle install # 未来升级可以用 bundle update
        {% endhighlight %}

如果执行过程中出现“安装某版本nokogiri失败，找不到libxml2本地库”，需要加参数先独立安装一下失败的nokogiri版本（然后再重试上一步）：
        {% highlight sh %}
gem install nokogiri -v '1.6.6.2' -- --with-xml2-include=/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.10.sdk/usr/include/libxml2 --use-system-libraries
        {% endhighlight %}

#### 4.使用bundler启动jekyll服务
        {% highlight sh %}
bundle exec jekyll serve # 启动并默认监听本地4000端口
        {% endhighlight %}
然后就可以访问 [http://127.0.0.1:4000/](http://127.0.0.1:4000/) 了，jekyll会自动watch目录变化并自动rebuild。  
写文章（post）的详情将在下一篇里讲。

### 四、部署博客到github

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
#### 3.以后如果换了新机器，先把博客克隆回来即可
        {% highlight sh %}
git clone https://github.com/watchzerg/watchzerg.github.io.git ~/myblog
        {% endhighlight %}
---
[《博客搭建(一) Github 初步配置》]({% post_url 2015-03-09-github-config %})
[《博客搭建(二) Jekyll与Github-page的安装和部署》]({% post_url 2015-03-10-jekyll-github-page-install-deploy %})
[《博客搭建(三) Jekyll配置》]({% post_url 2015-03-19-jekyll-config %})
[《博客搭建(四) 使用Jekyll写博客》]({% post_url 2015-03-20-jekyll-write-blog %})
