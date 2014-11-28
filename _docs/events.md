---
layout: docs
title: 3. 事件 
prev_section: templates
next_section: deploy 
permalink: /docs/events/
---

在client目录下创建文件`jubo-shell.js`，并写入以下代码：

{% highlight js %}
// jubo-shell.js
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
  }
});

Template.input.events({
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


