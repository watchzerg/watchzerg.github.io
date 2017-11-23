---
layout: post
title: "博客搭建(四) 使用Jekyll写博客"
tags: jekyll blog config tutorial
---

### 一、博文文件头
1,在_posts目录下新建`yyyy-MM-dd-titlepart1-titlepart2.md`这样的文件（不要带BOM头，特别是windows用户要注意）。例如本篇博客就是`2015-03-20-jekyll-write-blog.md`

2,文件开头必须是`YAML Front Matter`，用来标明本篇博客的一些属性，例如这篇博客的开头五行是：
{% highlight yaml %}
---
layout: post  # 表示这个文件需要按照“博客文章”的布局转换为html页面
title: "Jekyll的简单使用"
tags: jekyll blog config tutorial  # 空格隔开的标签，也可以这样：[jekyll,blog]
---
{% endhighlight %}
详细定义可以参考：
[http://jekyllrb.com/docs/frontmatter/](http://jekyllrb.com/docs/frontmatter/)

### 二、博文正文
1,正文使用markdown语法编写，如果按照上面的配置，还可以使用github扩展的markdown语法。

2,如果想要引用自己博客的其它文章，例如：[《博客搭建(三) Jekyll配置》]({% post_url 2015-03-19-jekyll-config %})，可以这么写：(需要去掉`{`与`%`之间的空格)

    [《博客搭建(三) Jekyll配置》]({ % post_url 2015-03-19-jekyll-config %})

3,链接本地文件(需要去掉前两个`{`之间的空格)：
    
    ![My helpful screenshot]({ { site.url }}/assets/screenshot.jpg)

4,代码高亮（使用Liquid语法标记，它会根据配置决定使用哪种语法高亮器）(需要去掉`{`与`%`之间的空格)：

    { % highlight ruby linenos %}
		...
	{ % endhighlight %}

5,这里可以查看pygments支持高亮的语法列表：[http://pygments.org/docs/lexers/](http://pygments.org/docs/lexers/)

6,为了显示高亮的语法，有可能需要引入css文件：[https://github.com/mojombo/tpw/blob/master/css/syntax.css](https://github.com/mojombo/tpw/blob/master/css/syntax.css)
如果显示行数，可能还需要自己在syntax.css指定.lineno的样式

7,可以把代码写在gist里，然后这样引用(需要去掉`{`与`%`之间的空格)：

    { % gist 6289895 RCDropdownArrowView.h %}

详细定义可以参考：
[http://jekyllrb.com/docs/posts/](http://jekyllrb.com/docs/posts/)

---
[《博客搭建(一) Github 初步配置》]({% post_url 2015-03-09-github-config %})  
[《博客搭建(二) Jekyll与Github-page的安装和部署》]({% post_url 2015-03-10-jekyll-github-page-install-deploy %})  
[《博客搭建(三) Jekyll配置》]({% post_url 2015-03-19-jekyll-config %})  
[《博客搭建(四) 使用Jekyll写博客》]({% post_url 2015-03-20-jekyll-write-blog %})  

