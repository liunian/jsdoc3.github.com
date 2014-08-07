---
title: JSDoc3 入门
description: 使用 JSDoc 来为 JavaScript 生成教程的快速入门教程。
---

## 始

JSDoc 3 是一个类似 JavaDoc 和 PHPDoc 的 JavaScript 文档生成器。直接在代码中按照指定方式添加文档注释，然后使用 JSDoc 工具可生成相应的 HTML 文档。

## 给代码添加文档注释

JSDoc 的目的是给 JavaScript 应用或库生成如命名空间、类、方法、函数参数等的 API 文档。

JSDoc 所用的注释必需刚好在所需要注释的代码的上方，且必需以 `/**` 开头， `/*`、`/***` 或更多的 * 号开始的就不被当做文档注释来解析，目的是不错误地解析普通注释内部的内容。

{% example "文档可以是简单的描述" %}

```js
/** This is a description of the foo function. */
function foo() {
}
```
{% endexample %}

添加描述很见简单，直接在文档注释内书写即可。

使用文档标签可提供更多的信息，如，可以添加一个标签来指明一个函数是一个构造器（constructor）。

{% example "使用文档标签来描述代码" %}

```js
/**
 * Represents a book.
 * @constructor
 */
function Book(title, author) {
}
```
{% endexample %}

可使用更多的标签来提供更多的信息，查阅标签文档来查看完整的支持标签。

{% example "使用标签来添加更多的信息" %}

```js
/**
 * Represents a book.
 * @constructor
 * @param {string} title - The title of the book.
 * @param {string} author - The author of the book.
 */
function Book(title, author) {
}
```
{% endexample %}

## 生成网站

代码添加了文档注释后就可以使用 JSDoc 3 来从代码中生成文档注释了。

JSDoc 默认会使用 `default` 模板来生成 html，可以根据需要来使用别的模板或创建新的模板。

{% example "使用命令来运行 JSDoc" %}

```
./jsdoc book.js
```
{% endexample %}

该命令将会在当前工作目录下创建 `out` 目录，在里面存放生成的 html 页面。
