---
tag: abstract
description: 该成员必需被子类实现或重写。
synonyms:
    - virtual
---

## 概览

`@abstract` 标签表示该成员必需被子类实现或重写。

## 示例

{% example "父类声明 `abstract` 方法，子类实现" %}

```js
/**
 * Generic dairy product.
 * @constructor
 */
function DairyProduct() {}

/**
 * Check whether the dairy product is solid at room temperature.
 * @abstract
 * @return {boolean}
 */
DairyProduct.prototype.isSolid = function() {
    throw new Error('must be implemented by subclass!');
};

/**
 * Cool, refreshing milk.
 * @constructor
 * @augments DairyProduct
 */
function Milk() {}

/**
 * Check whether milk is solid at room temperature.
 * @return {boolean} Always returns false.
 */
Milk.prototype.isSolid = function() {
    return false;
};
```
{% endexample %}
