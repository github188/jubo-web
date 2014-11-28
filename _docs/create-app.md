---
layout: docs
title: 1. 创建应用 
prev_section: home 
next_section: templates
permalink: /docs/create-app/
---

使用下面的命令来创建应用：

{% highlight bash %}
~ $ jubo create jubo-shell
{% endhighlight %}

这个命令会创建一个名字为jubo-shell的目录，目录里包含了应用所需的所有文件。

{% highlight bash %}
jubo-shell.css   # a CSS file to define your app's styles
jubo-shell.html  # an HTML file that defines view templates
jubo-shell.js    # a JavaScript file loaded on both client and server
.meteor          # internal Meteor files 
{% endhighlight %}

打开浏览器输入`http:/localhost:3000`就可以访问应用了，
你可以修改`jubo-shell.html`里的内容，比如`h1`标题，修改完成保存后，不需要刷新就可以在页面看到修改内容了。

对JuBo应用了有了初步体验之后，让我们开始jubo-shell的开发工作吧。
jubo-shell的源码发布在GitHub上，你可以获取[全部代码](https://github.com/jubolin/jubo-shell)。


