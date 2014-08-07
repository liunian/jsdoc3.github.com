---
tag: todo
description: 标明待完成的任务。
---

## 语法

`@todo text describing thing to do.`

## 概览

`@todo` 标签用于指明某部分代码中待完成的任务，可以同一个文档注释中多次使用。

## 示例

{% example "使用 @todo 标签" %}

```js
/**
 * @todo Write the documentation.
 * @todo Implement this function.
 */
function foo() {
    // write me
}
```
{% endexample %}
