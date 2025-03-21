---
title: id-match
rule_type: suggestion
---


> "There are only two hard things in Computer Science: cache invalidation and naming things." — Phil Karlton

Naming things consistently in a project is an often underestimated aspect of code creation.
When done correctly, it can save your team hours of unnecessary head scratching and misdirections.
This rule allows you to precisely define and enforce the variables and function names on your team should use.
No more limiting yourself to camelCase, snake_case, PascalCase, or HungarianNotation. `id-match` has all your needs covered!

## Rule Details

This rule requires identifiers in assignments and `function` definitions to match a specified regular expression.

## Options

This rule has a string option for the specified regular expression.

For example, to enforce a camelcase naming convention:

```json
{
    "id-match": ["error", "^[a-z]+([A-Z][a-z]+)*$"]
}
```

Examples of **incorrect** code for this rule with the `"^[a-z]+([A-Z][a-z]+)*$"` option:

::: incorrect

```js
/*eslint id-match: ["error", "^[a-z]+([A-Z][a-z]+)*$"]*/

const my_favorite_color = "#112C85";
const _myFavoriteColor  = "#112C85";
const myFavoriteColor_  = "#112C85";
const MY_FAVORITE_COLOR = "#112C85";
function do_something() {
    // ...
}

class My_Class {}

class myClass {
    do_something() {}
}

class anotherClass {
    #do_something() {}
}
```

:::

Examples of **correct** code for this rule with the `"^[a-z]+([A-Z][a-z]+)*$"` option:

::: correct

```js
/*eslint id-match: ["error", "^[a-z]+([A-Z][a-z]+)*$"]*/

const myFavoriteColor   = "#112C85";
const foo = bar.baz_boom;
const buz = { qux: bar.baz_boom };
do_something();
const obj = {
    my_pref: 1
};

class myClass {}

class anotherClass {
    doSomething() {}
}

class oneMoreClass {
    #doSomething() {}
}
```

:::

This rule has an object option:

* `"properties": false` (default) does not check object properties
* `"properties": true` requires object literal properties and member expression assignment properties to match the specified regular expression
* `"classFields": false` (default) does not check class field names
* `"classFields": true` requires class field names to match the specified regular expression
* `"onlyDeclarations": false` (default) requires all variable names to match the specified regular expression
* `"onlyDeclarations": true` requires only `var`, `const`, `let`, `function`, and `class` declarations to match the specified regular expression
* `"ignoreDestructuring": false` (default) enforces `id-match` for destructured identifiers
* `"ignoreDestructuring": true` does not check destructured identifiers

### properties

Examples of **incorrect** code for this rule with the `"^[a-z]+([A-Z][a-z]+)*$", { "properties": true }` options:

::: incorrect

```js
/*eslint id-match: ["error", "^[a-z]+([A-Z][a-z]+)*$", { "properties": true }]*/

const obj = {
    my_pref: 1
};

obj.do_something = function() {
    // ...
};
```

:::

### classFields

Examples of **incorrect** code for this rule with the `"^[a-z]+([A-Z][a-z]+)*$", { "classFields": true }` options:

::: incorrect

```js
/*eslint id-match: ["error", "^[a-z]+([A-Z][a-z]+)*$", { "classFields": true }]*/

class myClass {
    my_pref = 1;
}

class anotherClass {
    #my_pref = 1;
}
```

:::

### onlyDeclarations

Examples of **correct** code for this rule with the `"^[a-z]+([A-Z][a-z]+)*$", { "onlyDeclarations": true }` options:

::: correct

```js
/*eslint id-match: [2, "^[a-z]+([A-Z][a-z]+)*$", { "onlyDeclarations": true }]*/

foo = __dirname;
```

:::

### ignoreDestructuring: false

Examples of **incorrect** code for this rule with the default `"^[^_]+$", { "ignoreDestructuring": false }` option:

::: incorrect

```js
/*eslint id-match: [2, "^[^_]+$", { "ignoreDestructuring": false }]*/

const { category_id } = query;

const { categoryid_Default = 1 } = query;

const { category_ids: category_ids } = query;

const { category_id: category_Alias } = query;

const { category_id: category_IdRenamed, ...other_Props } = query;
```

:::

### ignoreDestructuring: true

Examples of **incorrect** code for this rule with the `"^[^_]+$", { "ignoreDestructuring": true }` option:

::: incorrect

```js
/*eslint id-match: [2, "^[^_]+$", { "ignoreDestructuring": true }]*/

const { category_id: category_alias } = query;

const { category_id: category_Id, ...other_props } = query;
```

:::

Examples of **correct** code for this rule with the `"^[^_]+$", { "ignoreDestructuring": true }` option:

::: correct

```js
/*eslint id-match: [2, "^[^_]+$", { "ignoreDestructuring": true }]*/

const { category_id } = query;

const { category_Id = 1 } = query;

const { category_alias: category_alias } = query;
```

:::

## When Not To Use It

If you don't want to enforce any particular naming convention for all identifiers, or your naming convention is too complex to be enforced by configuring this rule, then you should not enable this rule.
