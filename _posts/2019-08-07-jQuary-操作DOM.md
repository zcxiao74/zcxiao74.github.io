---
layout: post
title: "JQuery操作DOM"
date: 2019-08-07
tags: HTML  
---
## 修改css

高亮显示：`$('#test-css li.dy>span').css('background-color', '#ffd351').css('color', 'red');`

```
var div = $('#test-div');
div.css('color'); // '#000033', 获取CSS属性
div.css('color', '#336699'); // 设置CSS属性
div.css('color', ''); // 清除CSS属性
```

```
var div = $('#test-div');
div.hasClass('highlight'); // false， class是否包含highlight
div.addClass('highlight'); // 添加highlight这个class
div.removeClass('highlight'); // 删除highlight这个class
```



## 显示和隐藏DOM

```
var a = $('a[target=_blank]');
a.hide(); // 隐藏
a.show(); // 显示
```



### 获取DOM信息

```
// 浏览器可视窗口大小:
$(window).width(); // 800
$(window).height(); // 600

// HTML文档大小:
$(document).width(); // 800
$(document).height(); // 3500

// 某个div的大小:
var div = $('#test-div');
div.width(); // 600
div.height(); // 300
div.width(400); // 设置CSS属性 width: 400px，是否生效要看CSS是否有效
div.height('200px'); // 设置CSS属性 height: 200px，是否生效要看CSS是否有效
```



`attr()`和`removeAttr()`方法用于操作DOM节点的属性：

```
// <div id="test-div" name="Test" start="1">...</div>
var div = $('#test-div');
div.attr('data'); // undefined, 属性不存在
div.attr('name'); // 'Test'
div.attr('name', 'Hello'); // div的name属性变为'Hello'
div.removeAttr('name'); // 删除name属性
div.attr('name'); // undefined
```



`attr()`和`prop()`对于属性`checked`处理有所不同：

```
var radio = $('#test-radio');
radio.attr('checked'); // 'checked'
radio.prop('checked'); // true
radio.is(':checked'); // true
radio.is(':selected')
```



## 操作表单

```
input.val(); // 'test'
input.val('abc@example.com'); // 文本框的内容已变为abc@example.com

select.val(); // 'BJ'
select.val('SH'); // 选择框已变为Shanghai

textarea.val(); // 'Hello'
textarea.val('Hi'); // 文本区域已更新为'Hi'
```



## 添加DOM

```
// 添加DOM对象:
var ps = document.createElement('li');
ps.innerHTML = '<span>Pascal</span>';
var ul = $('#test-div>ul');
ul.append(ps);

// 添加jQuery对象:
ul.append($('#scheme'));

// 添加函数对象:
ul.append(function (index, html) {
    return '<li><span>Language - ' + index + '</span></li>';
});

//添加到指定元素之后
var js = $('#test-div>ul>li:first-child');
js.after('<li><span>Lua</span></li>');
```



## 删除节点

```
var li = $('#test-div>ul>li');
li.remove(); // 所有<li>全被删除
```