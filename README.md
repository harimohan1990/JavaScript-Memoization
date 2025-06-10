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

function memoize<T extends (...args: any[]) => any>(fn: T): T {
  const cache = new Map<string, ReturnType<T>>();

  return function (...args: Parameters<T>): ReturnType<T> {
    const key = JSON.stringify(args);
    if (cache.has(key)) {
      return cache.get(key)!;
    }

    const result = fn(...args);
    cache.set(key, result);
    return result;
  } as T;
}


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

#realtime example 

// ✅ TypeScript Memoization - Real-World Example

```ts
// Define a Product type
type Product = {
  id: number;
  name: string;
};

// Generate a large list of products
const products: Product[] = Array.from({ length: 10000 }, (_, i) => ({
  id: i,
  name: `Product ${i}`,
}));

// Generic memoization function using Map
function memoize<T extends (...args: any[]) => any>(fn: T): T {
  const cache = new Map<string, ReturnType<T>>();

  return function (...args: Parameters<T>): ReturnType<T> {
    const key = JSON.stringify(args);
    if (cache.has(key)) return cache.get(key)!;
    const result = fn(...args);
    cache.set(key, result);
    return result;
  } as T;
}

// Memoized search function
const filterProducts = memoize((query: string): Product[] => {
  return products.filter(p =>
    p.name.toLowerCase().includes(query.toLowerCase())
  );
});

// Simulate real-time search
console.log('First call (not cached):', filterProducts("product 123"));
console.log('Second call (cached):', filterProducts("product 123"));


Here are the **top memoization interview questions** with brief answers — ideal for JavaScript/TypeScript roles:

---

### ✅ **Basic Memoization Questions**

1. **What is memoization?**

   * A technique to cache function results for previously seen inputs to avoid redundant computation.

2. **How is memoization different from caching?**

   * Memoization is function-specific caching, whereas caching is a broader concept (e.g., HTTP cache, localStorage, etc.).

3. **What kind of functions benefit most from memoization?**

   * Pure, deterministic, and expensive functions (e.g., recursion, API transformations).

---

### ⚙️ **Practical & Code-Based Questions**

4. **Implement a memoization function in JavaScript/TypeScript.**

   * Ask to build a `memoize(fn)` wrapper with a cache (Map/object).

5. **How would you memoize a recursive Fibonacci function?**

   * Modify `fib(n)` to cache results or use dynamic programming.

6. **Why would you use `Map` over plain object for memoization?**

   * `Map` preserves key types and order, and handles complex keys better.

7. **How would you memoize a function with object arguments?**

   * Use `WeakMap` or serialize keys using `JSON.stringify()` (with caution).

---

### 🧠 **Advanced/Behavioral Questions**

8. **What are the space-time tradeoffs in memoization?**

   * Saves time by using more memory (O(n) space for cache).

9. **When should you avoid memoization?**

   * For non-pure functions, large datasets, or rapidly changing inputs.

10. **How does memoization differ from `useMemo` in React?**

* `memoize()` caches across calls; `useMemo` caches across renders based on deps.

---

Let me know if you'd like:

* A coding challenge version
* React-specific memoization questions
* Answers with diagrams or visual explanations


