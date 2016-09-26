# enforce either `module.exports` or `exports` (exports-style)

`module.exports` and `exports` are the same instance by default.
But those come to be different if one of them is modified.

```js
module.exports = {
    foo: 1
}

exports.bar = 2
```

In this case, `exports.bar` will be lost since only the instance of `module.exports` will be exported.

## Rule Details

This rule enforces the export style.

If you use `module.exports`, this rule disallows `exports`.<br>
If you use `exports`, this rule disallows `module.exports`.

You can select it by an option.

## Options

This rule has a string option.

```json
{
    "exports-style": [
        "error",
        "module.exports" or "exports",
        {
            "allowBatchAssign": false
        }
    ]
}
```

- `"module.exports"` (default) requires `module.exports` and disallows `exports`.
- `"exports"` requires `exports` and disallows `module.exports`.
- `allowBatchAssign` (default is `false`) allows `module.exports = exports = obj` if this is `true`.

Examples of **incorrect** code for the `"module.exports"` option:

```js
/*eslint exports-style: ["error", "module.exports"]*/

exports.foo = 1
exports.bar = 2
```

Examples of **correct** code for the `"module.exports"` option:

```js
/*eslint exports-style: ["error", "module.exports"]*/

module.exports = {
    foo: 1,
    bar: 2
}

module.exports.baz = 3
```

Examples of **incorrect** code for the `"exports"` option:

```js
/*eslint exports-style: ["error", "exports"]*/

module.exports = {
    foo: 1,
    bar: 2
}

module.exports.baz = 3
```

Examples of **correct** code for the `"exports"` option:

```js
/*eslint exports-style: ["error", "exports"]*/

exports.foo = 1
exports.bar = 2
```

Examples of **correct** code for the `"exports"` and `{"allowBatchAssign": true}` option:

```js
/*eslint exports-style: ["error", "exports", {"allowBatchAssign": true}]*/

// Allow `module.exports` in the same assignment expression as `exports`.
module.exports = exports = function foo() {
    // do something.
}

exports.bar = 1
```