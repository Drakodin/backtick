# backtick
Sometimes JavaScript can get a bit *weird*. As in, some things just don't make any sense in how they look, but it works nonetheless. Here, I'll demonstrate the one I find the most unsettling: tag functions.

## Notice
As it turns out, I'm not the first one to notice this. Take a look [wtfjs](https://github.com/denysdovhan/wtfjs) for a bunch of cool things.

## What are tag functions?
In JavaScript, we have what are called "template strings". These are strings that can have their values replaced by existing variables or other objects with a string conversion. In other languages, we would call this "format strings". Examples include `printf("value %d", 2)` in C and `f'{string}'` in Python. In JS, they look like this:
```js
let a = `Template ${'string'}`
```
where `a` is now `"Template string"` as the value "string" was inserted into the formatted string.

JS supports what are called "tag functions" that take template strings as a parameter, but in a very odd way. Let's take a look a basic tag function.
```js
function foo(strings, token) {
  console.log(token);
  return strings
}
```
All tag functions will first have a parameter that tokenizes the input template string using the "tags" (basically anything wrapped with `${}`) as separators. So for example, calling
```js
foo`Foo${'bar'}`
```
will net `strings` as `["Foo", ""]` and `token` as `"bar"`. The last element in `strings` will always be an empty string.

### Wait! There's no parentheses!
Exactly. That is what is odd with tag functions. You don't need to use parentheses in order to use them like a function, just a template string.
