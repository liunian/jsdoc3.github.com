---
title: JSDoc3 的名称路径（namepaths）
description: JSDoc3 名称路径使用指南。
related:
    - about-inline-tags.html
    - tags-link.html
---

## JSDoc 3 中的名称路径（Namepaths）

每个 JavaScript 变量需要有唯一标识，这样才能在文档中引用。名称路径除了能唯一标识外，还能区分实例成员、静态成员和内部变量。

{% example "JSDoc3 名称路径基本语法示例" %}

```
myFunction
MyConstructor
MyConstructor#instanceMember
MyConstructor.staticMember
MyConstructor~innerMember // note that JSDoc 2 uses a dash
```
{% endexample %}

下面示例中中演示了 3 个完全独立的方法：实例方法 `say`，内部函数 `say` 和静态方法 `say`。

{% example "使用文档 tag 来描述代码" %}

```js
/** @constructor */
Person = function() {
    this.say = function() {
        return "I'm an instance.";
    }

    function say() {
        return "I'm inner.";
    }
}
Person.say = function() {
    return "I'm static.";
}

var p = new Person();
p.say();      // I'm an instance.
Person.say(); // I'm static.
// there is no way to directly access the inner function from here
```
{% endexample %}

可以使用三中不同的名称路径来引用对应的方法：

{% example "使用文档 tag 来描述代码" %}

```
Person#say  // the instance method named "say."
Person.say  // the static method named "say."
Person~say  // the inner method named "say."
```
{% endexample %}

你可能会好奇为什么给不能外部访问的内部函数提供了引用语法。虽然 `~` 语法很少用，但因为一个方法可以返回一个内部函数的引用，所以可以引用内部函数。

如果一个构造器的实例方法也是一个构造器，那么可以简单地链成一个长路径：

{% example "使用文档 tag 来描述代码" %}

```js
/** @constructor */
Person = function() {
    /** @constructor */
    this.Idea = function() {
        this.consider = function(){
            return "hmmm";
        }
    }
}

var p = new Person();
var i = new p.Idea();
i.consider();
```
{% endexample %}

对于上面代码，可以使用 `Person#Idea#consider` 来引用 `consider` 方法。

This chaining can be used with any combination of the connecting symbols: `# . ~`
这种链式可用于 `# . ~` 中任一个符号。

{% example "特别地：模块、外部引用和事件" %}

```js
/** A module. Its name is module:foo/bar.
 * @module foo/bar
 */
/** The built in string object. Its name is external:String.
 * @external String
 */
/** An event. Its name is module:foo/bar.event:MyEvent.
 * @event module:foo/bar.event:MyEvent
 */
```
{% endexample %}

有一些特别的名称路径，如用 `module:` 标识的 [@module][module-tag]，`@external` 标识的 [@external][external-tag] 和 `event:` 标识的 [@event][event-tag]。

{% example "对象名称含有特殊字符的名称路径" %}

```js
/** @namespace */
var chat = {
    /**
     * Refer to this by {@link chat."#channel"}.
     * @namespace
     */
    "#channel": {
        /**
         * Refer to this by {@link chat."#channel".open}.
         * @type {boolean}
         * @defaultvalue
         */
        open: true,
        /**
         * Internal quotes have to be escaped by backslash. This is
         * {@link chat."#channel"."say-\"hello\""}.
         */
        'say-"hello"': function (msg) {}
    }
};

/**
 * Now we define an event in our {@link chat."#channel"} namespace.
 * @event chat."#channel"."op:announce-motd"
 */
```
{% endexample %}

Above is an example of a namespace with "unusual" characters in its member names (the hash character, dashes, even quotes).
To refer to these you just need quote the names: chat."#channel", chat."#channel"."op:announce-motd", and so on.
Internal quotes in names should be escaped with backslashes: chat."#channel"."say-\"hello\"".
上面示例是一个其成员名带有特殊字符（#、- 和引号）的命名空间，引用这些含有特殊字符的成员只需要用双引号包住，如 `chat."#channel"`、`chat."#channel"."op:announce-motd"`，名称自带的引号需要转义，如 `chat."#channel"."say-\"hello\""`。

[event-tag]: tags-event.html
[external-tag]: tags-external.html
[module-tag]: tags-module.html
