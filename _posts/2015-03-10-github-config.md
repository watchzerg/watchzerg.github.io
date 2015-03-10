---
layout: post
title: "Github 初步配置"
tags: github config tutorial
---

先写一篇测试博客看看。 
注册github账户就不说了，这里列一下配置github的过程吧（以mac为例）。 

### 一、ssh的配置
官方并不推荐，不过还是弄一下备用，而且key也可以用在其它地方。 
 
#### 1.生成ssh-key（最好设置密码，密码可以保存在key-chain里）：
        {% highlight sh %}
          ssh-keygen -t rsa -C "your_email@example.com"
        {% endhighlight %}
#### 2.增删改ssh-key密码：  
        {% highlight sh %}
        ssh-keygen -p 
        {% endhighlight %}
#### 3.在OS X里，ssh-agent已经集成在了key-chain里面，确保其在运行：
        {% highlight sh %}
          ssh-agent -s
        {% endhighlight %}
其默认会保护`.ssh/id_rsa`, `.ssh/id_dsa`, `.ssh/identity`这三个文件

#### 4.如果key名字不是默认，手工添加：
        {% highlight sh %}
          ssh-add -K path/to/my_key
        {% endhighlight %}
#### 5.拷贝公钥：
        {% highlight sh %}
          pbcopy < ~/.ssh/id_rsa.pub
        {% endhighlight %}
#### 6.粘贴到： [https://github.com/settings/ssh](https://github.com/settings/ssh)

#### 7.验证是否成功：
        {% highlight sh %}
          ssh -T git@github.com
        {% endhighlight %}


### 二、使用key-chain保存https访问密码
github官方建议使用https方式clone，所以需要使用credential helper将github密码缓存在git里。
如果使用homebrew安装的git，那么osxkeychain helper已经被安装了
#### 1.确认是否被安装：
        {% highlight sh %}
          git credential-osxkeychain
        {% endhighlight %}
#### 2.如果没有安装：
        {% highlight sh %}
curl -s -O https://github-media-downloads.s3.amazonaws.com/osx/git-credential-osxkeychain
sudo mv git-credential-osxkeychain "$(dirname $(which git))/git-credential-osxkeychain"
        {% endhighlight %}
#### 3.配置git使用helper：
        {% highlight sh %}
          git config --global credential.helper osxkeychain
        {% endhighlight %}
