---
tag: version
description: 给一项内容添加版本号。
related:
    - tags-since.html
---

## 概览

使用 `@version` 来给一项内容来添加版本号，标签后的内容即是版本号。

## 示例

{% example "使用 @version 标签" %}

```js
/**
 * Solves equations of the form a * x = b. Returns the value
 * of x.
 * @version 1.2.3
 * @tutorial solver
 */
function solver(a, b) {
    return b / a;
}
```
{% endexample %}
