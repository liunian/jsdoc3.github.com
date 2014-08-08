---
tag: class
description: 该函数应用 `new` 的方式来调用。
synonyms:
    - constructor
related:
    - tags-constructs.html
---

## 语法

`@class [<type> <name>]`


## 概览

`@class` 标签标明该函数是一个构造器，应用 `new` 关键字来创建实例。


## 示例

{% example "一个构造 Person 实例的函数。" %}

```js
/**
 * Creates a new Person.
 * @class
 */
function Person() {
}

var p = new Person();
```
{% endexample %}
