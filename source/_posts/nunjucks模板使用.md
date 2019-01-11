---
title: nunjucks模板使用
date: 2019-01-09 16:51:28
tags: 【nunjucks】
---

### 关于 Nunjucks

JavaScript 专用的功能丰富、强大的模板引擎。Nunjucks 是 jinja2 的 javascript 的实现，所以如果此文档有什么缺失，你可以直接查看 jinja2 的文档，不过两者之间还存在一些差异。

> [Nunjucks](https://nunjucks.bootcss.com/) 是一款 JavaScript 模板引擎，因为想基于[thinkjs](https://thinkjs.org/doc/index.html)搭建一个简单的项目部署系统，又不想前后端分离，页面逻辑比较简单，`thinkjs`原本又预设的 Nunjucks 作为模板引擎，所以决定使用这个来搭建，在此记录下使用方法。

### 使用

#### 文件扩展名

虽然你可以用任意扩展名来命名你的 Nunjucks 模版或文件，但 Nunjucks 社区还是推荐使用.njk。
如果你在给 Nunjucks 开发工具或是编辑器上的语法插件时，请记得使用.njk 扩展名。

#### 变量

在 thinkjs 中的 `controller` 中定义变量：

```js
async indexAction() {
    this.assign({
        title: "部署项目"
    });
    let data = {
      name: "abc",
      str: "fajsdf,fjaljewr,faj",
      array: [1, 23, 14, 123],
      action: {
        run: "300m"
      }
    };
    this.assign(data);
    return await this.display("index.njk");
}
```

变量会从模板上下文获取，写入方式和 vue 是一样的：
也可以像 javascript 一样获取变量的属性 (可使用点操作符或者中括号操作符)：

```html
{{ name }} {{ str }} {{array | join("|")}} {{ action.run }}{{ action["run"] }}
```

如果变量的值为 undefined 或 null 将不显示

#### 过滤器

过滤器是一些可以执行变量的函数，通过管道操作符 (|) 调用，并可接受参数。

```html
{{array | join("|")}}
```

#### 模板继承

模板继承可以达到模板复用的效果，当写一个模板的时候可以定义 "blocks"，子模板可以覆盖他，同时支持多层继承。

```html
<!-- commom.njk -->
{% block header %}
This is the default content
{% endblock %}

<section class="left">
  {% block left %}{% endblock %}
</section>

<section class="right">
  {% block right %}
  This is more content
  {% endblock %}
</section>

```

```html
<!-- index.njk -->
{% extends "commom.njk" %}

{% block left %}
This is the left side!
{% endblock %}

{% block right %}
This is the right side!
{% endblock %}
```
渲染结果：
```html
This is the default content

<section class="left">
  This is the left side!
</section>

<section class="right">
  This is the right side!
</section>
```

继承的模板也可以设为一个变量，这样就可以动态指定继承的模板。

##### super
如果想将父级区块中的内容渲染到子区块中可以通过调用super。
```
{% block right %}
{{ super() }}
Right side!
{% endblock %}
```
渲染结果：
```
This is more content
Right side!
```

#### 标签

##### if
```
{% if hungry %}
  I am hungry
{% elif tired %}
  I am tired
{% else %}
  I am good!
{% endif %}
```

##### for
for 可以遍历数组 (arrays) 和对象 (dictionaries)。
```js
var items = [{ title: "foo", id: 1 }, { title: "bar", id: 2}];
```
```html
<h1>Posts</h1>
<ul>
{% for item in items %}
  <li>{{ item.title }}</li>
{% else %}
  <li>This would display if the 'item' collection were empty</li>
{% endfor %}
</ul>
```
遍历对象：
```js
var food = {
  'ketchup': '5 tbsp',
  'mustard': '1 tbsp',
  'pickle': '0 tbsp'
};
```
```html
{% for ingredient, amount in food %}
  Use {{ amount }} of {{ ingredient }}
{% endfor %}
```
二维数组：
```js
var points = [[0, 1, 2], [5, 6, 7], [12, 13, 14]];
```
```html
{% for x, y, z in points %}
  Point: {{ x }}, {{ y }}, {{ z }}
{% endfor %}
```
在循环中可获取一些特殊的变量

- `loop.index`: 当前循环数 (1 indexed)
- `loop.index0`: 当前循环数 (0 indexed)
- `loop.revindex`: 当前循环数，从后往前 (1 indexed)
- `loop.revindex0`: 当前循环数，从后往前 (0 based)
- `loop.first`: 是否第一个
- `loop.last`: 是否最后一个
- `loop.length`: 总数

##### macro
宏 (macro) 可以定义可复用的内容，类似与编程语言中的函数，看下面的示例：
```html
{% macro field(name, value='', type='text') %}
<div class="field">
  <input type="{{ type }}" name="{{ name }}"
         value="{{ value | escape }}" />
</div>
{% endmacro %}
<!-- 现在 field 可以当作函数一样使用了： -->
{{ field('user') }}
{{ field('pass', type='password') }}
```
还可以从其他模板 import 宏，可以使宏在整个项目中复用。

##### set
set 可以设置和修改变量。
```html
{{name}}
{% set name = "123"%}
{{name}}
{% set x, y, z = 5 %}
```
如果在顶级作用域使用 set，将会改变全局的上下文中的值。如果只在某个作用域 (像是include或是macro) 中使用，则只会影响该作用域。

##### include
include 可引入其他的模板，可以在多模板之间共享一些小模板，如果某个模板已使用了继承那么 include 将会非常有用。
```html
{% include "item.html" %}
```
可在循环中引入模板
```html
{% for item in items %}
{% include "item.html" %}
{% endfor %}
```
可以使用ignore missing来略过异常，使模板文件不存在时不要抛出异常：
```html
{% include "missing.html" ignore missing %}
```

##### import
import 可加载不同的模板，可使你操作模板输出的数据，模板将会输出宏 (macro) 和在顶级作用域进行的赋值 (使用 set)。
```html
{% macro field(name, value='', type='text') %}
<div class="field">
  <input type="{{ type }}" name="{{ name }}"
         value="{{ value | escape }}" />
</div>
{% endmacro %}

{% macro label(text) %}
<div>
  <label>{{ text }}</label>
</div>
{% endmacro %}
```
可以 import 这个模板并将模板的输出绑定到变量 forms 上，然后就可以使用这个变量了：
```html
{% import "forms.html" as forms %}

{{ forms.label('Username') }}
{{ forms.field('user') }}
{{ forms.label('Password') }}
{{ forms.field('pass', type='password') }}
```
