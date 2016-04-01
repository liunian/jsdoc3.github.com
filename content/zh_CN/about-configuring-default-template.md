---
title: 配置 JSDoc 的默认模板
description: 如何通过 JSDoc 的默认模板来定制输出结果。
related:
    - about-configuring-jsdoc.html
---

JSDoc 的默认模板提供了多个选项来供自定义外观和生成内容。

[创建一个配置文件][about-config]，然后设定相应的值即可启用这些选项。

[about-config]: about-configuring-jsdoc.html


## 生成美化版的源文件

默认情况下，JSDoc 的默认模板会生成美化后的源文件，并在文档中添加链接来指向相应的源文件。

JSDoc 3.3.0 及以后版本可通过把 `templates.default.outputSourceFile` 设置为 `false` 来禁用美化，同时也会移除掉文档中指向源文件的链接。


## 复制静态资源到输出目录

JSDoc 的默认模板会自动地把如 CSS 等静态文件复制到输出目录中。JSDoc 3.3.0 及后续版本还可以复制额外的静态文件，比如，文档中使用到的图片。

配置项如下：

+ `templates.default.staticFiles.include`：待复制的内容路径数据，子目录会递归处理。
+ `templates.default.staticFiles.exclude`：忽略的内容的路径数组。
+ `templates.default.staticFiles.includePattern`：指定待复制的内容的正则表达式，不指定则全部复制。
+ `templates.default.staticFiles.excludePattern`：指定忽略的内容的正则表达式，不指定则不排除。

{% example "复制图片目录到输出目录" %}

把 `./myproject/static` 里的所有静态文件复制到输出目录：

```json
{
  "templates": {
    "default": {
      "staticFiles": {
        "include": [
        	"./myproject/static"
        ]
      }
    }
  }
}
```

如果静态文件中有 `./myproject/static/img/screen.png` 这个文件，那么文档中则可以用 `<img src="img/screen.png">` 来展示。

{% endexample %}


## 在页面底部展示当前时间

JSDoc 的默认模板默认会在生成文档的底部展示当前时间。JSDoc 3.3.0 及后续版本可以通过把 `templates.default.includeDate` 设置为 `false` 来移除。


## 导航栏中展示完整名称

JSDoc 的默认模板默认展示符号的短命名，如 `my.namespace.MyClass` 展示为 `MyClass`。JSDoc 3.4.0 及后续版本可把 `templates.default.useLongnameInNav` 设置为 `true` 来展示完整名称。


## 覆盖默认模板的布局文件

默认模板是使用 `layout.tmpl` 来配置生成文档页面的头部和底部，包括需要加载的 CSS 和 JavaScript 文件。JSDoc 3.3.0 及后续版本可以通过指定自定义的 `layout.tmpl` 来自定义 CSS 和 JavaScript。

把 `templates.default.layoutFile` 设置为自定义布局文件路径来使用该功能，相对路径指定的文件将会按照 `config.json`、当前目录和 JSDoc 安装目录的顺序来搜索。
