---
title: 教程机制
description: 代码的长篇教程。
---

教程机制和 phpDocumentor 的类似，在简短的代码 API 文档外支持更长更有解释性的完整教程。

通过 `-u` 选项，可以让 JSDoc 在指定的目录中搜索扩展名为 .xml、.xhtml、.html 和 .htm 的文件来作为教程文件。同时，也支持 Markdown 文件，JSDoc 会自动把它们转换为 HTML 文件。

教程默认是顶级的，这些顶级教程将会在导航菜单中列出来。

## 配置

每个教程都可以用一个同名的 .js 或 .json 文件来支持额外的教程配置，其支持两个属性，如下：

+ `title` 用该属性值来覆盖默认的教程展示名，默认是教程文件名。
+ `children` 子教程集合标识

当一个教程有 `children` 属性时，其子教程将作为次级文章列在其目录下而不是顶级导航。

## 标识

每个教程用其文件名来作为标识（如，`test.html` 标识为 `test`）。无论如何改变教程的 title 属性，其标识符始终是 `test`。title 属性用于展示，文件名用于标识，这一设定使尽管显示名称可变但依然可以链接到指定的教程成为可能。

### @tutorial 标签

文档型部件（doclet）中可以通过 `@tutorial`（类似 `@link` 和 `@see`）来链接教程。

{% example "@tutorial 标签示例" %}

```js
/** * Description.
 *
 * @class
 * @tutorial test-tutorial
 */
```
{% endexample %}

`@tutorial` 标签页能在行内描述中使用。

{% example "Using the tutorial tag in a description" %}

```js
/**
 * Description {@tutorial test-tutorial}.
 *
 * @class
 */
```
{% endexample %}

## 教程内容

教程内容是通过 `resolveLinks()` 来处理的，这意味着可以在教程内容里使用 `{@link}` 和 `{@tutorial}` 标签，它们会想文档部件中的描述一样被处理。

{% example "在内容中使用 @tutorial" %}

```html
&lt;p>This is tutorial content. See {@link Class.create} for OOP info and {@tutorial class-create} tutorial.&lt;/p>
```
{% endexample %}

## 向后兼容

这只是一个额外功能，意味着不开启 `-u` 功能时不会影响文档的构建。同时，模板的 `publish()` 方法并不是一个问题，因为教程只是最后一个参数，所以如果模板方法不对教程适用，那么则不处理。
