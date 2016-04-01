---
title: 包含 Package File
description: 如何在文档中展示包信息。
---

包文件包含的项目名称以及版本号等信息可用于项目文档，JSDoc 会自动地从项目文件 `package.json` 中提取信息来嵌入到文档中。默认的模板会在文档中展示项目名和版本号。

有两种方式来在文档中使用 `package.json`：

1. 在源码路径中包含 `package.json` 文件路径，JSDoc 将使用搜索到的第一个 `package.json` 文件。
2. 使用命令行参数 `-P/--package` 来指定 `package.json`，JSDoc 3.3.0 及后续版本有效。

`-P/--package` 优先，有该参数时忽略源码路径中找到的 `package.json` 文件。

`package.json` 必须符合 [npm 包格式][package-json]。

[package-json]: https://docs.npmjs.com/files/package.json


## Examples

{% example "源码路径中包含包文件" %}

```
jsdoc path/to/js path/to/package/package.json
```
{% endexample %}

{% example "使用 -P/--package 参数" %}

```
jsdoc --package path/to/package/package-docs.json path/to/js
```
{% endexample %}
