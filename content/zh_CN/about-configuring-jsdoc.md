---
title: 通过 conf.json 来配置 JSDoc
description: 如果使用配置文件来配置 JSDoc。
related:
    - about-commandline.html
    - about-plugins.html
    - plugins-markdown.html
---

## 配置文件

如果需要定制 JSDoc，那么可以用 `-c` 来指定一个 JSON 格式的配置文件，如 `jsdoc -c /path/to/conf.json`。

配置文件（一般命名为 conf.json）通过 JSON 格式来配置选项，JSDoc 安装目录 里的 conf.json.EXAMPLE 提供了一个简单的示例，并且，该文件也是缺省配置文件。

{% example %}
```js
{
    "tags": {
        "allowUnknownTags": true,
        "dictionaries": ["jsdoc","closure"]
    },
    "source": {
        "includePattern": ".+\\.js(doc)?$",
        "excludePattern": "(^|\\/|\\\\)_"
    },
    "plugins": [],
    "templates": {
        "cleverLinks": false,
        "monospaceLinks": false
    }
}
```
{% endexample %}

上述配置意味着：
+ JSDoc 支持不识别的标签（`tags.allowUnknownTags`）；
+ 同时支持 JSDoc 的标签和 [Closure Compiler 的标签][closure-tags] （`tags.dictionaries`）；
+ 仅处理扩展名为“.js”和“.jsdoc”的文件（`source.includePattern`）；
+ 忽略用下划线开头的文件和目录（`source.excludePattern`）；
+ 不使用任何插件（`plugins`）；
+ `@link` 标签渲染为普通文本（`templates.cleverLinks`，`templates.monospaceLinks`）。

下文会详述这些以及其它的配置项。

也可以添加各个插件或模板需要的配置项，比如 [Markdown 插件][markdown] 可用的 "markdown" 配置项。

[closure-tags]: https://developers.google.com/closure/compiler/docs/js-for-compiler#tags
[markdown]: plugins-markdown.html


## 指定输入文件

`source` 下的配置和命令行里传入的参数结合决定了 JSDoc 对哪些源文件生成文档（下面的示例实际试用中需要移除注释）。

{% example %}

```js
"source": {
    "include": [ /* 待生成文档的文件路径数组 */ ],
    "exclude": [ /* 忽略的文件路径数组 */ ],
    "includePattern": ".+\\.js(doc)?$",
    "excludePattern": "(^|\\/|\\\\)_"
}
```
{% endexample %}

+ `source.include`：可选，一个用来指定待生成文档的文件路径数组。命令行中传入的路径会和 JSDoc 扫描得到的配置文件合并。如果路径是一个目录，那么可以用 `-r` 参数来开启递归查找。
+ `source.exclude`：可选，一个用来指定待忽略的文件的路径数组。JSDoc 3.3.0 及后续版本中，这个数组可以包含 `source.include` 中的子目录。
+ `source.includePattern`：可选字符串，解析为正则表达式。如果有，那么所有文件名必需匹配该正则才会生成文档。默认值 `.+\\.js(doc)?$` 标明仅支持扩展名为 `.js` 或 `.jsdoc` 的文件。
+ `source.excludePattern`：可选字符串，解析为正则表达式。如果有，匹配到的文件都将忽略。默认设置是忽略掉用下划线开头的文件和目录。

配置项的生效步骤如下：

1. 查找所有 `source.include` 指定的文件，如果是目录，可以用 `-r` 来指定递归查找。
2. 如果指定了正则表达式 `source.includePattern`，那么对于步骤 1 找到的每一个文件，如果不匹配正则表达式，那么排除。
3. 如果指定了正则表达式 `source.excludePattern`，那么步骤 2 中过滤后文件，如果匹配了当前正则表达式，那么排除。
4. 步骤 3 过滤后的文件，如果路径在 `source.exclude` 中，那么排除。

JSDoc 会解析上述步骤完成后得到的所有文件。

如对于一下目录结构：

{% example %}

```
myProject/
|- a.js
|- b.js
|- c.js
|- _private
|  |- a.js
|- lib/
   |- a.js
   |- ignore.js
   |- d.txt
```
{% endexample %}

在自定义 `conf.json` 中配置如下 `source`：

{% example %}

```js
"source": {
    "include": [ "myProject/a.js", "myProject/lib", "myProject/_private" ],
    "exclude": [ "myProject/lib/ignore.js" ],
    "includePattern": ".+\\.js(doc)?$",
    "excludePattern": "(^|\\/|\\\\)_"
}
```
{% endexample %}

然后在 `myProject` 目录中运行 JSDoc：

{% example %}

```
jsdoc myProject/c.js -c /path/to/my/conf.json -r
```
{% endexample %}

JSDoc 会对下面文件生成文档：

+ `myProject/a.js`
+ `myProject/c.js`
+ `myProject/lib/a.js`

原因是：

1. 根据 `source.include` 和命令行指定的路径，我们有下面这些文件
    + `myProject/c.js` (来自命令行)
    + `myProject/a.js` (来自 `source.include`)
    + `myProject/lib/a.js`, `myProject/lib/ignore.js`, `myProject/lib/d.txt` (来自使用了 `-r` 的 `source.include`)
    + `myProject/_private/a.js` (来自 `source.include`)
2. 应用 `source.includePattern`，排除掉 `myProject/lib/d.txt`（扩展名不是 .js 或 .jsdoc）。
3. 应用 `source.excludePattern`，排除掉 `myProject/_private/a.js`。
4. 应用 `source.exclude`，排除掉 `myProject/lib/ignore.js`。


## 在配置文件中插入命令行参数

可以在配置文件中放置[命令行参数][options]而不用用命令行的形式来传递。具体来说，是在配置文件 conf.json 的 `opts` 项中用相关参数的长命名方式来配置。

[options]: about-commandline.html

{% example "在配置文件中配置命令行参数" %}

```js
"opts": {
    "template": "templates/default",  // same as -t templates/default
    "encoding": "utf8",               // same as -e utf8
    "destination": "./out/",          // same as -d ./out/
    "recurse": true,                  // same as -r
    "tutorials": "path/to/tutorials", // same as -u path/to/tutorials
}
```
{% endexample %}

因为有了 `source.include` 和 `opts` 配置，所以可以把 JSDoc 的所有参数都移到配置文件中，这样，运行命令可以简化为：

```
jsdoc -c /path/to/conf.json
```

同时在命令行和配置文件中指定命令行参数的情况，命令行中指定的优先。


## 插件

把插件相对于 JSDoc 目录的路径添加到 `plugins` 数组即可使用插件。

下面示例中使用了 Markdown 和 summarize 插件，前者把 Markdown 文件转为 HTML，后者对每个文档生成概述。

{% example %}

```
"plugins": [
    "plugins/markdown",
    "plugins/summarize"
]
```
{% endexample %}

[插件指南][plugins]提供了更加详细的信息，JSDoc 在 `jsdoc/plugins` 中提供了内置的插件。

Markdown 插件是通过在 conf.json 中添加 `markdown` 字段来配置，详细查看[配置 Markdown 插件][markdown]。

[plugins]: about-plugins.html
[markdown]: plugins-markdown.html


## 定制输出风格

可通过 `template` 选项来改变生成内容的外观，但自定义模板可能不使用这些选项，参考 [配置 JSDoc 默认模板][default-template]来获取更多的默认模板支持信息。

{% example %}

```js
"templates": {
    "cleverLinks": false,
    "monospaceLinks": false
}
```
{% endexample %}

若 `templates.monospaceLinks` 设为 true，所有 [@link][link-tag] 标签的链接文字将使用等宽字体。

若 `templates.cleverLinks` 设为 true，对于 {@link asdf}，如果 asdf 是链接，那么使用普通字体，否则使用等宽字体。如，`{@link http://github.com}` 会使用普通字体，而 `{@link MyNamespace.myFunction}` 则使用等宽字体。

若 `templates.cleverLinks` 为 true，那么 `templates.monospaceLinks` 将被忽略。

可以通过 `{@linkcode ...}` 和 `{@linkplain ...}` 来强制指定渲染风格，具体查看 [@link, @linkcode and @linkplain][link-tag]。

[default-template]: about-configuring-default-template.html
[link-tag]: tags-inline-link.html


## 标签和标签字典

配置中的 `tags` 选项控制了合法标签的范围以及标签的解析方式。

{% example %}

```js
"tags": {
    "allowUnknownTags": true,
    "dictionaries": ["jsdoc","closure"]
}
```
{% endexample %}

`tags.allowUnknownTags` 属性影响 JSDoc 对于不识别的标签的处理方式。如果是 `false`，那么在碰到不识别的标签（如 `@foo`）时会输出警告。默认是 `true`。

`tags.dictionaries` 属性指定了合法标签库及解析方式。JSDoc 3.3.0 及后续版本又两个内置的字典：

+ `jsdoc`：JSDoc 核心标签。
+ `closure`：[Closure Compiler 标签][closure-tags].

默认同时支持两个字典，并且优先使用在前面的 `jsdoc`。

If you are using JSDoc with a Closure Compiler project, and you want to avoid using tags that
Closure Compiler does not recognize, change the `tags.dictionaries` setting to `["closure"]`. You
can also change this setting to `["closure","jsdoc"]` if you want to allow core JSDoc tags, but you
want to ensure that Closure Compiler-specific tags are interpreted as Closure Compiler would
interpret them.
如果只想支持 Closure Compiler，那么把 `tags.dictionaries` 设为 `["closure"]`；如果想支持两者且 Closure Compiler 优先，那么设为 `["closure","jsdoc"]`。

[closure-tags]: https://developers.google.com/closure/compiler/docs/js-for-compiler#tags
