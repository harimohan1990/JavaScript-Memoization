# JavaScript-Memoization

### ⚡ JavaScript Memoization – Quick Guide

**Memoization** is a performance optimization technique that stores results of expensive function calls and returns the cached result when the same inputs occur again.

---

### ✅ Basic Memoization Function

```js
function memoize(fn) {
  const cache = {};
  return function (...args) {
    const key = JSON.stringify(args);
    if (cache[key]) return cache[key];
    const result = fn(...args);
    cache[key] = result;
    return result;
  };
}
```

**Usage:**

```js
const slowAdd = (a, b) => {
  console.log('Calculating...');
  return a + b;
};

const memoizedAdd = memoize(slowAdd);

memoizedAdd(1, 2); // Calculating... → 3
memoizedAdd(1, 2); // Cached → 3
```

---

### 🧠 When to Use

* Expensive computations (e.g. Fibonacci, factorial)
* Pure functions (no side effects)
* Repeated calls with same inputs

---

### 🔁 Recursive Memoization Example

```js
const fib = memoize(function(n) {
  if (n <= 1) return n;
  return fib(n - 1) + fib(n - 2);
});

fib(40); // Much faster with memoization
```


### ⚡ JavaScript Memoization – Quick Guide

**Memoization** is a performance optimization technique that stores results of expensive function calls and returns the cached result when the same inputs occur again.

---

### ✅ Basic Memoization Function

```js
function memoize(fn) {
  const cache = {};
  return function (...args) {
    const key = JSON.stringify(args);
    if (cache[key]) return cache[key];
    const result = fn(...args);
    cache[key] = result;
    return result;
  };
}
```

**Usage:**

```js
const slowAdd = (a, b) => {
  console.log('Calculating...');
  return a + b;
};

const memoizedAdd = memoize(slowAdd);

memoizedAdd(1, 2); // Calculating... → 3
memoizedAdd(1, 2); // Cached → 3
```

---

### 🧠 When to Use

* Expensive computations (e.g. Fibonacci, factorial)
* Pure functions (no side effects)
* Repeated calls with same inputs

---

### 🔁 Recursive Memoization Example

```js
const fib = memoize(function(n) {
  if (n <= 1) return n;
  return fib(n - 1) + fib(n - 2);
});

fib(40); // Much faster with memoization
```

---

