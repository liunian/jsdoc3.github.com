---
tag: constructs
description: 该函数成员将被视为前面的 class 的构造器。
related:
    - tags-lends.html
---

## 概览

当使用对象字面量来定义一个类时（如 `@lends` 标签），`@constructs` 可用于标明某个函数将被用来构造类实例。


## 语法

`@constructs [<name>]`


## Examples

{% example "配合 @lends 使用 @constructs 标签" %}

```js
var Person = makeClass(
    /** @lends Person.prototype */
    {
        /** @constructs */
        initialize: function(name) {
            this.name = name;
        },
        /** Describe me. */
        say: function(message) {
            return this.name + " says: " + message;
        }
    }
);
```
{% endexample %}

{% example "无 @lends 时必需提供类名" %}

```js
makeClass('Menu',
    /**
     * @constructs Menu
     * @param items
     */
    function (items) { },
    {
        /** @memberof Menu# */
        show: function(){
        }
    }
);
```
{% endexample %}
