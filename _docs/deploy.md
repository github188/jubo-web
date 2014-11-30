---
layout: docs
title: 4. 发布 
prev_section: events 
next_section: next 
permalink: /docs/deploy/
---

到目前为止我们已经完成了jubo-shell应用的开发，进入应用目录输入`jubo`在本地运行jubo-shell应用，
然后通过浏览器访问`127.0.0.1:3000`就可以使用本地的jubo-shell应用了。

我们也可以通过下面的命令把应用发布到无线路由器,这样就可以在PC、手机和平板上通过Shell命令来控制路由器了。

{% highlight sh %}
~ $ jubo deploy root@devip
{% endhighlight %}

`devip`是路由器的管理IP，应用发布成功后，我们就可以访问`devip:22786`来体验应用了。
应用默认是发布到`/root`目录下的，你也可以使用`root@devip:path`来指定发布路径。

