---
tag: access
description: 说明成员的访问权限（private、public 或 protected）。
related:
    - tags-global.html
    - tags-instance.html
    - tags-private.html
    - tags-protected.html
    - tags-public.html
    - tags-static.html
---

## 语法

`@access <private|protected|public>`

## 概览

`@access` 标签标明成员的访问权限。其中，`@access private` 等同于 `@private`，`@access protected` 等同于 `@protected`，`@access public` 等同于 `@public` 或直接不使用以上标签。私有成员（private）只有在开启 `--private` 选项才会输出到文档中。

注意，文档部件的 _访问权限_ 和 _作用域（scope）_ 是两回事。如，即使 `Parent` 内的一个局部变量 `child` 被注释为 `@public`，但 `child` 依然被视为局部变量，其命名空间是 `Parent~child`。如若需要改变文档部件的作用域，参考 [@instance][instance-tag]、 [@static][static-tag] 和 [@global][global-tag] 标签。

[global-tag]: tags-global.html
[instance-tag]: tags-instance.html
[static-tag]: tags-static.html


## 示例

{% example "@access is a synonym for @private, @protected, @public." %}

```js
/** @constructor */
function Thingy() {

    /** @access private */
    var foo = 0;

    /** @access protected */
    this._bar = 1;

    /** @access public */
    this.pez = 2;

}

// same as...

/** @constructor */
function OtherThingy() {

    /** @private */
    var foo = 0;

    /** @protected */
    this._bar = 1;

    /** @public */
    this.pez = 2;

}
```
{% endexample %}
