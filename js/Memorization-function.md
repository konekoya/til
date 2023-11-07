# Memorization function

Memorization is a common technique for caching heavy calculations to reduce the time and resources required for re-calculation. The actual implementation is based on a LeetCode medium-level question

```js
const memorized = (fn, value) => {
  const cache = {};

  return () => {
    const key = String(value);

    if (key in cache) {
      console.log("Found cached value, returning it. Its key name: " + key);
      return cache[key];
    }

    console.log(
      "No cached value found in the object, run the calculation fn..."
    );
    const result = fn();
    cache[key] = result;

    return result;
  };
};

const value = 10000000;

// Simulate the heavy calculation with a large loop
const fn = () =>
  Array(value)
    .fill(0)
    .map((x) => x + 1);

// Get the memorized function 
const r = memorized(fn, value);

// Record the time it takes to run the calculation
console.time("List");
const list = r();
console.timeEnd("List");

console.log(list[0]);

console.time("New list");
const newList = r();

// The second run should be much quicker since it's a cached value
console.timeEnd("New list");

console.log(list[0]);
```

