---
title: no-dupe-args
rule_type: problem
handled_by_typescript: true
---



If more than one parameter has the same name in a function definition, the last occurrence "shadows" the preceding occurrences. A duplicated name might be a typing error.

## Rule Details

This rule disallows duplicate parameter names in function declarations or expressions. It does not apply to arrow functions or class methods, because the parser reports the error.

If ESLint parses code in strict mode, the parser (instead of this rule) reports the error.

Examples of **incorrect** code for this rule:

::: incorrect { "sourceType": "script" }

```js
/*eslint no-dupe-args: "error"*/

function foo(a, b, a) {
    console.log("value of the second a:", a);
}

const bar = function (a, b, a) {
    console.log("value of the second a:", a);
};
```

:::

Examples of **correct** code for this rule:

::: correct { "sourceType": "script" }

```js
/*eslint no-dupe-args: "error"*/

function foo(a, b, c) {
    console.log(a, b, c);
}

const bar = function (a, b, c) {
    console.log(a, b, c);
};
```

:::
