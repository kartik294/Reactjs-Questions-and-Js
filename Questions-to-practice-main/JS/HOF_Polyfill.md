<a id="top"></a>

# Polyfills of some important higher order functions

1.  [Array.protoype.map](#map)

2.  [Array.prototype.filter](#filter)

3.  [Array.prototype.reduce](#reduce)

4.  [Array.prototype.forEach](#foreach)

5.  [Promise.all](#promise-all)

6.  [Promise.allSettled](#promise-allSettled)

7.  [Promise.race](#promise-race)

8.  [Promise.any](#promise-any)

**Map**
<a id="map">

```javascript
Array.prototype.ourMap = function (
  callback,
  thisArg
) {
  let arr = [];

  for (let i = 0; i < this.length; i++)
    arr.push(
      callback.call(thisArg, this[i], i, this)
    );

  return arr;
};
```

</a>

[back to top ⬆️](#top)

**Filter**
<a id="filter">

```javascript
Array.prototype.ourFilter = function (
  callback,
  thisArg
) {
  let arr = [];

  for (let i = 0; i < this.length; i++)
    if (callback.call(thisArg, this[i], i, this))
      arr.push(this[i]);

  return arr;
};
```

</a>

[back to top ⬆️](#top)

**Reduce**
<a id="reduce">

```javascript
Array.prototype.ourReduce = function (
  callback,
  initialVal
) {
 if (!initialValue && this.length === 0)
    throw new Error("Empty array with no initial value");

  let sum = initialVal??0;

  for (let i = 0; i < this.length; i++) {
      sum = callback(sum, this[i], i, this);
  }

  return sum;
};
```

</a>

[back to top ⬆️](#top)

**forEach**
<a id="foreach">

```javascript
Array.prototype.ownEach = function (
  callback,
  thisArg
) {
  for (i = 0; i < this.length; i++)
    callback.call(thisArg, this[i], i, this);
};
```

</a>

[back to top ⬆️](#top)

**Promise.all**
<a id="promise-all"></a>

```javascript
Promise.customAll = (promises) =>
  new Promise((resolve, reject) => {
    let results = [];
    let n = promises.length;
    let completed_promises = 0;

    promises.forEach(async (promise, idx) => {
      try {
        const res = await promise;
        results[idx] = res;
        completed_promises++;

        if (completed_promises === n)
          resolve(results);
      } catch (err) {
        reject(err);
      }
    });
  });
```



[back to top ⬆️](#top)

**Promise.allSettled**

<a id="promise-allSettled"></a>

```javascript
Promise.myAllSettled = (promises) =>
  new Promise((resolve) => {
    let results = [];
    let n = promises.length;
    let promises_settled = 0;

    promises.forEach(async (promise, idx) => {
      try {
        const res = await promise;
        results[idx] = {
          status: "fulfilled",
          value: res,
        };
      } catch (err) {
        results[idx] = {
          status: "rejected",
          value: err,
        };
      } finally {
        promises_settled++;

        if (promises_settled === n)
          resolve(results);
      }
    });
  });
```



[back to top ⬆️](#top)

**Promise.race**

<a id="promise-race"></a>

```javascript
Promise.myRace = (promises) =>
  new Promise((resolve, reject) => {
    promises.forEach((promise) => {
      Promise.resolve(promise)
        .then(resolve)
        .catch(reject);
    });
  });
```



[back to top ⬆️](#top)

**Promise.any**

<a id="promise-any"></a>

```javascript
Promise.myAny = (promises) =>
  new Promise((resolve, reject) => {
    let n = promises.length;

if(n===0)
  rej(new AggregateError([],"All promises were rejected"))

    let total_errors = Array.from({ length: n });
    let error_count = 0;

    promises.forEach(async (promise, idx) => {
      try {
        const res = await promise;
        resolve(res);
      } catch (err) {
        error_count++;
        total_errors[idx] = err;

        if (error_count === n)
          reject(new AggregateError(total_errors,"All promises were rejected));
      }
    });
  });
```


