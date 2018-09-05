### jQuery中$.fn的用法

$.fn是指jquery的命名空间，加上fn上的方法及属性，会对jquery实例每一个有效。 如扩展$.fn.abc(),即**$.fn.abc()是对jquery扩展了一个abc方法,那么后面你的每一个jquery实例都可以引用这个方法了：$("#div").abc();**

* $.fn.function用于添加单个方法  
* $.fn.extend 用于添加多个方法  

```JavaScript
$.fn.abc = function() {}
$.fn.extend({
  abc: function() {}
});
```
效果都是一样的


jQuery为开发插件提拱了两个方法，分别是：
* jQuery.extend(object);为扩展jQuery类本身.为类添加新的方法。
* jQuery.fn.extend(object);给jQuery对象添加方法。

##### $.fn.function
fn是什么?。查看jQuery代码，

```JavaScript
jQuery.fn = jQuery.prototype ={
　　　init: function( selector, context ){//....　
　　　//......
};
```
jQuery.fn =jQuery.prototype   
jQuery是一个封装得非常好的类，比如我们用语句　$("#btn1") 会生成一个 jQuery类的实例。实例就可以使用prototype

#### jQuery.fn.extend(object);  

比如我们要开发一个插件，做一个特殊的编辑框，当它被点击时，便alert当前编辑框里的内容。可以这么做：
```JavaScript
$.fn.extend({

  alertWhileClick:function(){

    $(this).click(function(){

      alert($(this).val());
    });
  }
});
```

> **$.fn.function**和**jQuery.fn.extend(object)**对jQuery.prototype进得扩展，就是为jQuery类添加“成员函数”。jQuery类的实例可以使用这个“成员函数”。

##### jQuery.extend(object);
　
>为jQuery类添加添加类方法，可以理解为添加静态方法。

```JavaScript
$.extend({
　　add:function(a,b){returna+b;}
});
```
便为jQuery添加一个为add的“静态方法”，之后便可以在引入jQuery的地方，使用这个方法了，

```JavaScript
$.add(3,4); //return 7
```
