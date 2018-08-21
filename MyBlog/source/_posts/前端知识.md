---
title: 前端知识.md
date: 2018-08-17 17:53:44
tags: 
  - toastr(吐司)
categories:
  - 前端
  - toastr
  - 弹窗式通知
---
# toastr入门与基本使用

## toastr概述

 jquery toastr 一款轻量级的通知提示框插件。
  网页开发中经常会用到提示框，自带的alert样式无法调整，用户体验差。
  所以一般通过自定义提示框来实现弹窗提示信息，而jquery toastr正是为此的一款非常棒的插件
 
 ## 整体认知
 
  我们可以通过**toastr**的[**Demo网址**](https://codeseven.github.io/toastr/demo.html)来整体认识一下toastr的作用，以及toastr的实现。然后我们通过[**toastr官网**](https://codeseven.github.io/toastr/)来得到更多的链接以及使用方法。项目中使用toastr我们一般引入整个源，然后使用，这里我们先下载[**toastr源码**](https://github.com/CodeSeven/toastr)
  
## 使用方法

### 三个步骤

**引入模块类库**

```html
<link href="toastr.css" rel="stylesheet" type="text/css" />
<script src="jquery-1.9.1.min.js"></script>
<!-- jquery文件，必须先引入的模块类库 -->
<script src="toastr.js"></script>
```

**直接使用API调用,看到演示**
```html
<script src="jquery-1.9.1.min.js"></script>
<!-- jquery文件，必须先引入的模块 -->
<link href="toastr.css" rel="stylesheet"/>
<script src="toastr.js"></script>
<!--显示一个信息没有标题-->
toastr.info('Are you the 6 fingered man?')
```
**其他选项**    
- 显示一个警告,没有标题
```html
toastr.warning('My name is Inigo Montoya. You killed my father', 'prepare to die!')
```
- 显示一个成功,标题
```html
toastr.success('Have fun storming the castle!', 'Miracle Max Says')
```
- 显示错误标题
```html
toastr.error('I do not think that word means what you think it means.', 'Inconceivable!')
```
- 清除当前的列表
```html
toastr.clear()
```

## 整体集成效果

- 先引入模块

```html
<link href="toastr.css" rel="stylesheet" type="text/css" />
<script src="jquery-1.9.1.min.js"></script>
<!-- jquery文件，必须先引入的模块类库 -->
<script src="toastr.js"></script>
```
- 编写HTML页面引用

```html
<button id="showtoast">show info toast（提示）</button>
<br>
<button id="showtoastsuccess">show success toast（成功）</button>
<br>
<button id="showtoasterror">show error toast（错误）</button>
<br>
<button id="showtoastwarning">show warning toast（警告）</button>
<br>
<button id="cleartoasts">clear toast（清除）</button>
<br>
<button id="removetoasts">remove toast（移除）</button>
<br>
```

- 编写JS脚本语言

```javascript
<script type="text/javascript">
    $(function() {
        //设置显示配置
        var messageOpts = {
            "closeButton" : true,//是否显示关闭按钮
            "debug" : false,//是否使用debug模式
            "positionClass" : "toast-bottom-right",//弹出窗的位置
            "onclick" : null,
            "showDuration" : "300",//显示的动画时间
            "hideDuration" : "1000",//消失的动画时间
            "timeOut" : "5000",//展现时间
            "extendedTimeOut" : "1000",//加长展示时间
            "showEasing" : "swing",//显示时的动画缓冲方式
            "hideEasing" : "linear",//消失时的动画缓冲方式
            "showMethod" : "fadeIn",//显示时的动画方式
            "hideMethod" : "fadeOut" //消失时的动画方式
        };
        toastr.options = messageOpts;
        $('#showtoast').click(function() {
            //提示
            //调用方法1
            toastr.info('内容1');
            //调用方法2
            //toastr.info('内容2', '标题2');
            //调用方法3
            //toastr['info']('内容3', '标题3');
            //调用方法4
            //toastr.info('内容4', '标题4',messageOpts);
        });
        $('#showtoastsuccess').click(function() {
            //成功
            toastr.success('内容success', '标题success');
        });
        $('#showtoasterror').click(function() {
            //错误
            toastr.error('内容error', '标题error');
        });
        $('#showtoastwarning').click(function() {
            //警告
            toastr.warning('内容warning', '标题warning');
        });
        $('#cleartoasts').click(function() {
            //清除
            toastr.clear();
        });
        $('#removetoasts').click(function() {   
            //移除
            toastr.remove();
        });
    })
</script>
```

### 其他的可供选择的设置选项

```javascript
closeButton: true
//是否在通知弹窗上面显示关闭按钮，true：显示；false：不显示

debug: true
//是否开起debug

progressBar: false
//是否显示进度条，当为false时候不显示；当为true时候，显示进度条，当进度条缩短到0时候，消息通知弹窗消失

positionClass: 'toast-top-right'
//位置信息，消息弹窗显示的位置，可以显示的位置对应的值

toast-top-right
toast-botton-right
toash-bottom-left
toast-top-left
toast-top-full-width  //这个是在网页顶端，宽度铺满整个屏幕
toast-bottom-full-width
toast-top-center    //顶端中间
toast-bottom-center
onclick: null

showDuration: "300"
//显示动作（从无到有这个动作）持续的时间


hideDuration: "1000"
//隐藏动作持续的时间

timeOut: "5000"
//间隔的时间

extendedTimeOut: "1000"


showEasing: "swing",
hideEasing: "linear",
showMethod: "fadeIn"
//显示的方式，和jquery相同，可以是show()

hideMethod: "fadeOut"
//隐藏的方式，和jquery相同，可以是hide()


toastr['error']('I am yanying', 'title');
//其中的error为显示的通知的样式类型，有4种选择
```
success 成功，绿色
info 信息，蓝色
warning，警告，橙色
error，错误，深红色


 