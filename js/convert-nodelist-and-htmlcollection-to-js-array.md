# Convert NodeList and HTMLCollection to JS Array

A [NodeList](https://developer.mozilla.org/en-US/docs/Web/API/NodeList) object is a collection of nodes. It's returned from certain DOM API calls such as `document.querySelectorAll()`. NodeLists are not native JS array, although it can use `.foreach()` and a few [iterators](https://developer.mozilla.org/en-US/docs/Web/API/NodeList#instance_methods). We often need to convert it to JS array so we can use functional methods like `.map()`, `.filter()` or `.reduce` just to name a few.

```html
<ul class="states">
  <li>Illinois</li>
  <li>Indiana</li>
  <li>Idaho</li>
  <li>Ohio</li>
  <li>Mississippi</li>
  <li>Tennessee</li>
</ul>

<script>
  const states = document.querySelectorAll('.states > li');
  console.log(states); // NodeList(6) [li, li, li, li, li, li]
  console.log(Array.isArray(states)); // false

  const statesList = [...states]; // alternatively, use Array.from(states)
  console.log(statesList); // [li, li, li, li, li, li]
  console.log(Array.isArray(statesList)); // true
</script>
```

In the above example, we convert the NodeList to an array by using [Spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax). There is another method that does the exact conversion: `Array.from()`

Besides NodeLists, an older API like `document.getElementsByTagName()` returns [HTMLCollection](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCollection) which is even harder to work with as it just has a fewer API [available](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCollection), not even `.foreach()`. Fortunately, we can still covert it to an JS Array:

```html
<ul class="states">
  <li>Illinois</li>
  <li>Indiana</li>
  <li>Idaho</li>
  <li>Ohio</li>
  <li>Mississippi</li>
  <li>Tennessee</li>
</ul>

<script>
  const states = document.getElementsByTagName('li');
  console.log(states); // HTMLCollection(6) [li, li, li, li, li, li]
  console.log(Array.isArray(states)); // false

  const statesList = [...states];
  console.log(statesList); // [li, li, li, li, li, li]
  console.log(Array.isArray(statesList)); // true
</script>
```

In general, when working with DOMs, use modern APIs that give you back NodeLists instead of HTMLCollection.
