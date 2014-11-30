---
layout: docs
title: 2. 模板 
prev_section: create-app
next_section: events 
permalink: /docs/templates/
---	

开始编写代码之前，我们必须要正确的设置项目。
为了保证项目整洁，我们首先删除`jubo-shell.html`、`jubo-shell.js`和`jubo-shell.css`。

然后在`jubo-shell`目录下新建两个子文件夹:`client`和`server`。
在`client`目录下创建文件`jubo-shell.html`，并写入以下代码：

{% highlight html %}
  <!-- jubo-shell.html -->
  <head>                                                                                                                          
    <title>jubo-shell</title>
  </head>
  
  <body>
    <div class="container">
      {% raw %}{{> input}}{% endraw %}
      {% raw %}{{> buffer}}{% endraw %}
    </div>
  </body>
  
  <template name="input">
    <div class="row">
      <div class="input-group">
        <input type="text" class="form-control" id="cmd">
        <span class="input-group-btn">
          <button class="btn btn-primary" type="button">Run</button>
        </span>
      </div>
    </div>
  </template>
  
  <template name="buffer">
    <div class="row" id="buffer">
      <pre>{% raw %}{{ output }}{% endraw %}</pre>
    </div>
  </template>
{% endhighlight %}

关于文件，  JuBo有以下几条规则： 

* 在 /server 文件夹中的代码只会在服务器端运行。
* 在 /client 文件夹中的代码只会在客户端运行。
* 其它代码则将同时运行于服务器端和客户端上。
* 在 /lib 文件夹中的文件将被优先载入。
* 所有以 main.* 命名的文件将在其他文件载入后载入。
* 请将所有的静态文件（字体，图片等）放置在 /public 文件夹中。

> 这里的服务器端指的是OpenWrt设备，客户端指的是浏览器。

### HTML模板
Meteor会解析应用程序文件夹中的所有HTML文件，确定`<head>`，`<body>`和`<template>`三个顶级标记，并组成一个标准的HTML文件。

任何`<head>`标记包含的所有内容将被添加到HTML文件的`head`段，
同样，任何`<body>`标记包含的所有内容将被添加到HTML文件的`body`段。

Meteor模板将对`<template>`标记包含的代码进行编译，HTML可以通过`{% raw %}{{> templateName}}{% endraw %}`包含相关代码，
JavaScript文件可以通过`Template.templateName`进行引用。

#### 往模板中添加数据
我们可以通过定义`helpers`从JavaScript中传递数据给模板。
在这里我们定义了`Template.buffer.output`，并且从会话中获取数据或者使用默认数据。
这样我们就可以在HTML文件的`<template>`标记中通过`{% raw %}{{output}}{% endraw %}`来输出数据了。

#### 添加CSS
由于指南手册主要关注HTML和JavaScript ，所以为了避免在CSS细节上花费过多时间，这里提供完整的CSS文件。

{% highlight css %}
/* jubo-shell.css */
/* CSS declarations go here */ 
body {
  padding-top: 20px; 
}

#buffer {
  margin-top: 20px;
}

#cmd {
  font-weight:bold;
  font-size: 1.5em;
  padding-left: 20px; 
}

pre {
  font-size: 1.5em
}
{% endhighlight %}







