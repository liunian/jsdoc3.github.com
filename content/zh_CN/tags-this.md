---
tag: this
description: 此时 this 指向何处？
related:
    - tags-memberof.html
---

## 语法

`@this <namePath>`

## 概览

`@this` 标签指示在别的对象中使用时 `this` 关键字指向何处。

## 示例

下面示例中，`@this` 标签指明 `this.name` 是指 `Greeter#name` 而不是全局变量 `name`。

```js
/** @constructor */
function Greeter(name) {
    setName.apply(this, name);
}

/** @this Greeter */
function setName(name) {
    /** document me */
    this.name = name;
}
```
