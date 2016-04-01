---
title: 块标签和内联标签
description: 块标签和内联标签概述。
---

## 概述

JSDoc 支持两种类型的标签：

+ **块标签**, JSDoc 注释的顶层元素。
+ **内联标签**, 位于块标签或描述内。

块标签通常用来提供像函数形参这些代码详细信息，而内联标签则常像 HTML 中的 `<a>` 链接那样用来链接到文档中的其余部分。

块标签总是以 `@` 符号开头，并除了 JSDoc 注释中最后一个外，都必须以换行结束。

内联标签也必须以 `@` 开头，但标签及其携带内容必须包含在花括号（`{}`）中，如果携带内容本身需要有 `}`，那么则需要用 `\` 来转义。另，内联标签不需要用换行来结束。

大多数的 JSDoc 标签都是块标签。一般地，本文档中所说的标签都是指块标签。

## 示例

下面示例中，`@param` 是一个块标签，而 `{@link}` 则是一个内联标签：

{% example "JSDoc 注释内的块标签和内联标签" %}

```js
/**
 * Set the shoe's color. Use {@link Shoe#setSize} to set the shoe size.
 *
 * @param {string} color - The shoe's color.
 */
Shoe.prototype.setColor = function(color) {
    // ...
};
```
{% endexample %}

可以像上面那样在描述内使用内联标签，也可以像下面那样在块标签内使用：

{% example "块标签内的内联标签" %}

```js
/**
 * Set the shoe's color.
 *
 * @param {SHOE_COLORS} color - The shoe color. Must be an enumerated
 * value of {@link SHOE_COLORS}.
 */
Shoe.prototype.setColor = function(color) {
    // ...
};
```
{% endexample %}

多个块标签之间必须换行分隔：

{% example "用换行分隔的块标签" %}

```js
/**
 * Set the color and type of the shoelaces.
 *
 * @param {LACE_COLORS} color - The shoelace color.
 * @param {LACE_TYPES} type - The type of shoelace.
 */
Shoe.prototype.setLaceType = function(color, type) {
    // ...
};
```
{% endexample %}
