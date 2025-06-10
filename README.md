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



Here’s a complete set of **working code examples** showing how memoization is handled in both **React 18** and **React 19**:

---

## 🔷 **React 18: Manual Memoization**

```tsx
// React 18 Example (App.tsx)
import React, { useState, useMemo, useCallback } from 'react';

function ExpensiveComponent({ number }: { number: number }) {
  const computed = useMemo(() => {
    console.log('Computing...');
    return number ** 2;
  }, [number]);

  return <div>Square: {computed}</div>;
}

function App() {
  const [num, setNum] = useState(1);
  const [count, setCount] = useState(0);

  const increment = useCallback(() => setCount(c => c + 1), []);

  return (
    <div>
      <h2>React 18 Manual Memoization</h2>
      <input
        type="number"
        value={num}
        onChange={(e) => setNum(Number(e.target.value))}
      />
      <ExpensiveComponent number={num} />
      <button onClick={increment}>Clicked {count} times</button>
    </div>
  );
}

export default App;
```

---

## 🔶 **React 19: With Compiler (No Memo Needed)**

> In React 19 with the **React Compiler** (enabled by default in frameworks like Next.js 14), you can skip `useMemo` and `useCallback`.

```tsx
// React 19 Example (App.tsx)
// No useMemo or useCallback needed
import React, { useState } from 'react';

function ExpensiveComponent({ number }: { number: number }) {
  console.log('Computing...');
  const computed = number ** 2;

  return <div>Square: {computed}</div>;
}

function App() {
  const [num, setNum] = useState(1);
  const [count, setCount] = useState(0);

  return (
    <div>
      <h2>React 19 Auto Memoization (Compiler)</h2>
      <input
        type="number"
        value={num}
        onChange={(e) => setNum(Number(e.target.value))}
      />
      <ExpensiveComponent number={num} />
      <button onClick={() => setCount(c => c + 1)}>Clicked {count} times</button>
    </div>
  );
}

export default App;
```

---

### ✅ **Comparison**

| Feature            | React 18                           | React 19 with Compiler         |
| ------------------ | ---------------------------------- | ------------------------------ |
| `useMemo`          | Required for expensive computation | Usually unnecessary            |
| `useCallback`      | Required for stable refs           | Compiler handles automatically |
| `React.memo`       | Manual wrapping of components      | Often redundant with compiler  |
| Performance Tuning | Manual                             | Automatic & declarative        |

---


✅ Your complete working examples for **React 18 vs React 19 memoization** are now saved in the file **"React 18 Vs 19 Memoization"** in the canvas.

It includes:

* Manual memoization with `useMemo`, `useCallback` (React 18)
* Auto memoization using the React 19 Compiler (no hooks needed)

Great! Here's a quick follow-up based on your "sure" — I've listed options you can choose from next:

---

### ✅ What would you like next?

1. **📊 Performance Benchmark**
   Compare render counts & execution time of React 18 vs 19 memoization using:

   * `React.Profiler`
   * `console.time()`
   * Lighthouse metrics
  
     // React 18: Manual Memoization Example with Profiler and Timing
import React, { useState, useMemo, useCallback, Profiler } from 'react';

function ExpensiveComponent18({ number }: { number: number }) {
  console.time('React 18 compute');
  const computed = useMemo(() => {
    console.log('React 18: Computing...');
    const result = number ** 2;
    console.timeEnd('React 18 compute');
    return result;
  }, [number]);

  return <div>Square: {computed}</div>;
}

function onRenderCallback(
  id: string,
  phase: 'mount' | 'update',
  actualDuration: number
) {
  console.log(`[Profiler: ${id}] ${phase} took ${actualDuration}ms`);
}

export function React18App() {
  const [num, setNum] = useState(1);
  const [count, setCount] = useState(0);

  const increment = useCallback(() => setCount(c => c + 1), []);

  return (
    <div>
      <h2>React 18 Manual Memoization</h2>
      <input
        type="number"
        value={num}
        onChange={(e) => setNum(Number(e.target.value))}
      />
      <Profiler id="ExpensiveComponent18" onRender={onRenderCallback}>
        <ExpensiveComponent18 number={num} />
      </Profiler>
      <button onClick={increment}>Clicked {count} times</button>
    </div>
  );
}

// React 19: With Compiler - No Memo Needed (with Profiler and Timing)
import React19, { useState as useState19, Profiler as Profiler19 } from 'react';

function ExpensiveComponent19({ number }: { number: number }) {
  console.time('React 19 compute');
  console.log('React 19: Computing...');
  const computed = number ** 2;
  console.timeEnd('React 19 compute');
  return <div>Square: {computed}</div>;
}

function onRenderCallback19(
  id: string,
  phase: 'mount' | 'update',
  actualDuration: number
) {
  console.log(`[Profiler: ${id}] ${phase} took ${actualDuration}ms`);
}

export function React19App() {
  const [num, setNum] = useState19(1);
  const [count, setCount] = useState19(0);

  return (
    <div>
      <h2>React 19 Auto Memoization (Compiler)</h2>
      <input
        type="number"
        value={num}
        onChange={(e) => setNum(Number(e.target.value))}
      />
      <Profiler19 id="ExpensiveComponent19" onRender={onRenderCallback19}>
        <ExpensiveComponent19 number={num} />
      </Profiler19>
      <button onClick={() => setCount(c => c + 1)}>Clicked {count} times</button>
    </div>
  );
}

To evaluate **React 18 vs React 19 memoization** with **Lighthouse metrics**, here’s a step-by-step approach and what to look for in results:

---

## 🚀 Lighthouse Metrics for React 18 vs 19 Memoization

### ✅ **Key Metrics to Compare**

| Metric                   | What to Check                               |
| ------------------------ | ------------------------------------------- |
| **Performance**          | Time to interactive (TTI), main thread work |
| **Speed Index**          | How fast the page visually loads            |
| **Total Blocking Time**  | Time UI was blocked due to JS processing    |
| **Time to Interactive**  | When app becomes fully usable               |
| **JavaScript Execution** | Size and parse/compile time                 |

---

### 🧪 **How to Test with Lighthouse**

1. **Run locally with `npm run build && serve`** for production-like behavior.
2. Open Chrome DevTools → Lighthouse → Select **Performance + Best Practices**
3. Run Lighthouse on both apps:

   * React 18 app (`React18App`)
   * React 19 app (`React19App`)
4. Capture & compare:

   * TTI (Time to Interactive)
   * Total Blocking Time
   * JS execution time
   * FPS under interaction (devtools → Performance tab)

---

### 📊 **Expected Results**

| Aspect                   | React 18                         | React 19 (Compiler)                   |
| ------------------------ | -------------------------------- | ------------------------------------- |
| Re-renders               | Higher (if `useMemo` is missing) | Reduced due to compiler optimizations |
| JavaScript execution     | Slightly heavier                 | Lighter due to removed boilerplate    |
| Total blocking time      | Slightly higher                  | Lower due to async rendering          |
| DevTools Profiler Output | Manual hook usage needed         | Auto-optimized render behavior        |



2. **🧱 React.memo() Examples**
   Show how `React.memo()` compares to React 19 Compiler behavior with props and re-renders.

3. **⚛️ Integration in Next.js 14**
   How memoization and Server/Client components work with React Compiler in a real Next.js app.

4. **🧪 Interactive Demo App**
   A small playground app where you can toggle memoization on/off and observe differences.







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


