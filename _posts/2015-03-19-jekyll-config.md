---
layout: post
title: "博客搭建(三) Jekyll配置"
tags: jekyll blog writing tutorial
---

### 一、配置jekyll
修改根目录的`_config.yml`文件，上面哪些title、url等自己看着改。
我在下面又填了几行配置：
{% highlight yaml %}
markdown: kramdown  #使用kramdown做代码语法高亮
kramdown:
  input: GFM  #启用github的markdown语法
gems:
  - jekyll-sitemap  #生成sitemap
  - jekyll-mentions  #允许"@ somebody"
  - jemoji  #允许标签
{% endhighlight %}
详细配置可以参考:
[http://jekyllrb.com/docs/configuration/](http://jekyllrb.com/docs/configuration/)

### 二、加入google analytics
去[http://www.google.com/analytics/](http://www.google.com/analytics/)注册个帐号，按提示把js代码拷下来，放到`_includes/footer.html`文件的最后面（这样被其它layout包含时，实际在`</body>`标签前面）。

### 三、加入百度统计
去[http://tongji.baidu.com/](http://tongji.baidu.com/)注册个帐号，按提示把js代码拷下来，放到`_includes/head.html`文件的`</head>`标签之前（因为百度最新的统计代码是异步的，放到页面前面只是注册事件，延迟到页面加载完成后才会触发）

### 四、集成评论系统
这里使用disqus（也可以考虑国产的[`多说`](http://duoshuo.com/))
去[https://disqus.com/](https://disqus.com/)注册个帐号(可以选择关联facebook和twitter等账户)
然后到[https://disqus.com/admin/create/](https://disqus.com/admin/create/)按提示一步步的创建和定制针对自己博客的评论系统
点击Install之后，选择`Universal Code`，拷贝js代码，放到`_layouts/post.html`中的`</article>`前面。

### 五、自定义404页面
在根目录创建一个404.md文件
文件头这样写：
{% highlight yaml %}
---
layout: page
permalink: /404.html
---
{% endhighlight %}
文件内容就是自定义的404页面了
我这里用的[`益云`](http://www.iyiyun.com/)的公益404，特么好丑。
可是腾讯公益的404页代码考过来样式又会乱，暂时懒得搞，先放着。

### 六、自定义域名
我还没开搞
简单的来说：搜个godaddy的优惠码、注册域名、交给DNSPod解析、别名指向watchzerg.github.io（不要指向具体IP）
这些都比较简单了，以后补充
github官方也给出了很多自定义域名的建议
[https://help.github.com/categories/github-pages-basics/](https://help.github.com/categories/github-pages-basics/)

### 七、CDN加速
建议使用七牛云，咱这点流量是免费的，业界良心啊

---
[《博客搭建(一) Github 初步配置》]({% post_url 2015-03-09-github-config %})
[《博客搭建(二) Jekyll与Github-page的安装和部署》]({% post_url 2015-03-10-jekyll-github-page-install-deploy %})
[《博客搭建(三) Jekyll配置》]({% post_url 2015-03-19-jekyll-config %})
[《博客搭建(四) 使用Jekyll写博客》]({% post_url 2015-03-20-jekyll-write-blog %})





