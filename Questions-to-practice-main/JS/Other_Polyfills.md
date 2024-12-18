<a id="top"></a>

# Polyfills of some other functions

1. [Call](#call)
2. [Apply](#apply)
3. [Bind](#bind)

<a id="call">
</a>

```javascript
Function.prototype.myCall = function (
  thisArg,
  ...args
) {
  const context=thisArg || globalThis;

  context.fn = this;
  const result=context.fn(...args);
  delete context.fn;

  return result;
};
```


[⬆️ Top](#top)

<a id="apply"></a>

```javascript
Function.prototype.myApply = function (
  thisArg,
  args
) {
  const context=thisArg||globalThis;

  context.myMethod = this;
  const result=context.myMethod(...args);
  delete context.myMethod;

  return result;
};
```



[⬆️ Top](#top)

<a id="bind"></a>

```javascript
Function.prototype.myBind = function (
  thisArg,
  ...args
) {
  const context=thisArg||globalThis;
  thisArg.myMethod = this;

  return function () {
    thisArg.myMethod(...args);
  };
};
```


