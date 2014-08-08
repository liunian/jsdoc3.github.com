---
tag: author
description: 标明某段代码的作者。
related:
    - tags-file.html
    - tags-version.html
---

## 语法

`@author <name> [<emailAddress>]`


## 概览

`@author` 标签标明某段代码的作者。JSDoc 3.2 及之后，若作者名后跟着一个用尖括号（<>）包住的 email，默认的模板会吧该 email 转为 `mailto:` 链接。

> 译注： 同一处 `@author` 可使用多次。


## 示例

{% example "标明某段代码的作者" %}

```js
/**
 * @author Jane Smith <jsmith@example.com>
 */
function MyClass() {}
```
{% endexample %}
