---
title: JSDoc 命令行参数
description: 关于 JSDoc 的命令行参数。
related:
    - about-configuring-jsdoc.html
---

JSDoc 的基本使用方式如下：

    /path/to/jsdoc yourSourceCodeFile.js anotherSourceCodeFile.js ...

`...` 代表其它需要生成文档的源码文件路径。

另外，可以提供一个[MarkDown 文件][md-file]（后缀名为 .md）或一个“README”文件作为文档的首页，见此[参考文档][including-readme]。

JSDoc 支持一系列的可选参数，这些参数大多有长命名和短命名形式，也可以通过[配置文件][config-file]来设置参数。

可选参数|意义
------|-----------
`-c <value>`, `--configure <value>`|SDoc[配置文件][config-file]路径，默认是 JSDoc 安装目录下的 `conf.json` 或 `conf.json.EXAMPLE` 文件。
`-d <value>`, `--destination <value>`|生成文档的存放目录路径。对于 JSDoc 的内置 `Haruki` 模板，直接在 `console` 输出。默认是 `./out`。
`-e <value>`, `--encoding <value>`|源码文件的编码方式，默认是 `utf-8`。
`-h`, `--help`|查看 JSDoc 的命令行可选参数
`-l`, `--lenient`|在有错误时（如一个标签缺少了必需值）仍尝试继续生成文档。默认有错误时立刻终止并退出。
`--match <value>`|只运行有指定值 `value` 的测试。
`--nocolor`|执行测试时，不在终端中使用彩色文字。Windows 平台上默认开启该选项。
`-p`, `--private`|为 [`@private` 标签][tags-private] 字段生成文档。默认不生成。
`-q <value>`, `--query <value>`|供解析并存储于 `env.opts.query` 的查询字符串，如： `foo=bar&baz=true`.
`-r`, `--recurse`|递归处理。
`-t <value>`, `--template <value>`|用于生成文档的模板路径。默认是内置模板 `templates/default`。
`-T`, `--test`|执行 JSDoc 测试，并在终端输出测试结果
`-u <value>`, `--tutorials <value>`|JSDoc 查找教程的目录。若不提供，则不生成教程。参考[教程指引][tutorials]。
`-v`, `--version`|显示 JSDoc 的版本。
`--verbose`|执行测试时，显示详细信息。
`-X`, `--explain`|以 JSON 的形式显示文档结构。


[config-file]: about-configuring-jsdoc.html
[including-readme]: about-including-readme.html
[md-file]: http://daringfireball.net/projects/markdown/
[tags-private]: tags-private.html
[tutorials]: about-tutorials.html


## 示例

使用 `/path/to/my/conf.json` 配置来对 `./src` 目录里的代码生成文档，并输出到 `./docs` 目录：

{% example %}

```
/path/to/jsdoc src -r -c /path/to/my/conf.json -d docs
```
{% endexample %}

执行 JSDoc 所有的命名符合 `tag` 的测试，并输出各测试结果。

{% example %}

```
/path/to/jsdoc -T --match tag --verbose
```
{% endexample %}
