---
layout: docs
title: 3. 事件 
prev_section: templates
next_section: deploy 
permalink: /docs/events/
---

在client目录下创建文件`jubo-shell.js`，并写入以下代码：

{% highlight js %}
// client/jubo-shell.js
Template.buffer.output = function () {
  if (Session.get('output'))
    return Session.get('output');
  else
    return "JuBo Shell 0.0.1\n\n"
          +"This is a basic terminal, it will run Linux/Unix commands on OpenWrt device\n"
          +"and will print on the screen the output."
          +"\n\n"
          +"Notes: Can't support cd command\n"
          +"       Max output buffer is 200*1024." 

}

Template.input.events({
  'click button': function(evt) {
    var cmd  = $('#cmd').val();
    Meteor.call('jsh', cmd, function (err, data) {
      $('#cmd').val('');
      Session.set('output', data );
    });
  },
  
  'keypress input#cmd': function (evt) {
    if (evt.which === 13) { // enter key
      var cmd  = $('#cmd').val();
      Meteor.call('jsh', cmd, function (err, data) {
        $('#cmd').val('');
        Session.set('output', data );
      });
    }
  } 
});
{% endhighlight %}

我们可以通过Template.templateName.events来监听事件，这里我们监听了输入框的回车键和按钮的单击事件。
当用户按下回车或者按下按钮时，就会调用服务器端提供的`jsh`函数执行Shell命令，并通过Session输出结果。
Session 是一个全局的响应式数据存储。它全局性的意思是全局的单例对象：这个Session对象在全局都是可被访问到的。

在server目录下创建文件`jubo-shell.js`，并写入以下代码：

{% highlight js %}
// server/jubo-shell.js
var future = Npm.require('fibers/future');
var exec = Npm.require('child_process').exec;

Meteor.methods({
  jsh: function (command) {
    var shell = new future();

    exec(command,function(error,stdout,stderr){
      if(error) 
        shell.return('' + error);
      else
        shell.return('' + stdout);
    });

    return shell.wait();
  }
});
{% endhighlight %}

