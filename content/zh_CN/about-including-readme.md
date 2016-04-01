---
title: 用 JSDoc 3 引入 README 文件
description: 在文档中引入 README 文件的教程。
---

有两种方式在文档中插入 `README` 文档：

1. 在配置文件中扫描路径中添加 `README.md` 文件的路径。JSDoc 会使用找到的第一个 `README.md` 文件。
2. 用命令行参数 `-R/--readme` 来指定 `README` 文件。JSDoc 3.3.0 及后续版本才有这个功能，`README` 文件的文件名及扩展名都随意，但必须是 Markdown 格式。

如果使用了 `-R/--readme` 参数，那么 JSDoc 将优先使用该参数指定的文件而不是在源码目录里查找到的文件。

JSDoc 的默认模板会把 `README` 生成为 `index.html`。


## 示例

{% example "在源码路径中添加 README 文件" %}

```
jsdoc path/to/js path/to/readme/README.md
```
{% endexample %}

{% example "使用 -R/--readme 参数" %}

```
jsdoc --readme path/to/readme/README path/to/js
```
{% endexample %}
