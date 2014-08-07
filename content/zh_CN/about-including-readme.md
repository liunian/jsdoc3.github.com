---
title: 用 JSDoc 3 引入 Readme 文件
description: 在文档中引入 readme 文件的教程。
---

只需简单地在命令行参数中添加上 readme 文件的路径即可把该 readme 文件添加进文档中，并作为根据指定模板生成的网站个首页（`index.html`）。该文件必须是 markdown 文件，且扩展名为 `.md`。

{% example "Including a readme file in your documentation" %}

```
jsdoc C:\path\to\my\JS\project\sourceFiles C:\path\to\my\JS\project\README.md
```
{% endexample %}

如果 readme 文件被模板成功纳入，那么其内容就会在文件列表前被渲染成 HTML。
