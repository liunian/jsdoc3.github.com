---
tag: constant
description: 标明一个对象是常量。
synonyms:
    - const
related:
    - tags-default.html
    - tags-type.html
---

## S语法

`@constant [<type> <name>]`


## 概览

`@contant` 标签用于某个标识符是常量。


## 示例

下面将演示标识常量的用法。注意，尽管下面的代码中使用了 `const` 关键字，但这个不是 JSDoc 所必需的。如果 JavaScript 宿主环境不支持声明常量，`@const` 文档也可用于 `var` 的声明中。

{% example "一个代表红色的常量字符串" %}

```js
/** @constant
    @type {string}
    @default
*/
const RED = 'FF0000';

/** @constant {number} */
var ONE = 1;
```
{% endexample %}

注意，上述示例通过 `@type` 来提供了类型，但这个是可选的。另，`@default` 标签也是可选的，它会把所赋的值（如此处的 FF0000）添加到文档中。
