# -sass
该文章以我的经验角度向大家分享一些sass的实战使用方法，不定期更新，希望能帮助大家\<br> 
    每一个打算把sass当作自己项目css编译器的开发者在开发前都建议看看这篇文章，如果我讲到的你都用过，那么你可以回顾一下，如果没有用到，相信会对你的开发起到一定的帮助，如果还有更多的建议，非常欢迎提出来让大家共享。

#### 1.减少重复性工作

譬如下面这段代码，看起来极其类似，并且具有规律性，可以使用sass的each方法简化
```
.pdt10 {
    padding-top: 10px;
}
.pdt5 {
    padding-top: 5px;
}
.pdt0 {
    padding-top: 0px;
}
.pdr10 {
    padding-right: 10px;
}
.pdr5 {
    padding-right: 5px;
}
.pdr0 {
    padding-right: 0px;
}
.pdb10 {
    padding-bottom: 10px;
}
.pdb5 {
    padding-bottom: 5px;
}
.pdb0 {
    padding-bottom: 0px;
}
.pdl10 {
    padding-left: 10px;
}
.pdl5 {
    padding-left: 5px;
}
.pdl0 {
    padding-left: 0px;
}
```
简化后的代码如下：
```
@for $i from 0 through 3 {
    $mutiple: $i*5;
    $edgeSize: #{$i*5}px !important;
    $maps: (
        pdt: padding-top, 
        pdb: padding-bottom,
        pdl: padding-left,
        pdr: padding-right
    );
    @each $key, $value in $maps {
        .#{$key}#{$mutiple} {
            #{$value}: $edgeSize
        }
    }
}
```
#### 2.命名空间
当一个项目足够大到必须要考虑维护性的时候，你可以尝试给每一个组件或模块定义一个命名空间
以vue组件举个例子，你可以像如下代码一样去给组件样式命名
这样不仅能让代码看起来更加规范，也可以避免样式污染。
demo.vue
```
<template>
……
</template>
<script>
……
</script>
<style lang="scss">
$name: demo;
.#{$name}-container {
.#{$name}-header {
……
}
.#{$name}-content {
……
}
.#{$name}-footer {
……
}
}
</style>
```
还有一种更简洁的写法

demo.vue
```
<template>
……
</template>
<script>
……
</script>
<style lang="scss">
$name: demo;
.#{$name} {
&-header {
……
}
&-content {
……
}
&-footer {
……
}
}
</style>
```
这样是不是让自己的代码充满了一些灵性与仙气，美滋滋~

#### 3.定义公用方法组
比如多行文本溢出，三角形等都可以定义在方法组里面，这都是比较传统的用法了。
例子：


#### 4.混合与继承
@mixin通过 @include调用后解析出来的样式是以拷贝形式存在的，而下面的继承则是以联合声明的方式存在的，所以从3.2.0版本以后，建议传递参数的用 @mixin，而非传递参数类的使用下面的继承 %。

