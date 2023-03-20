# Get All Elements From a Form

An HTML form may contain elements like `input`, `select` or `textarea`. When working with JavaScript, you can grab all elements of a particular form by using: `form:elements`

```html
<h1>Login</h1>
<form action="">
  <input type="text" value="" placeholder="name" />
  <input type="password" value="" placeholder="password" />
  <hr />
  <button type="submit">Login</button>
  <button>Reset</button>
</form>

<script>
  const form = document.querySelector('form');

  // Get all elements within the form
  const elements = form.elements;

  // HTMLFormControlsCollection(4) [input, input, button, button]
  console.log(elements);

  // Since it's an `HTMLFormControlsCollection`, we need to convert it to an JS array
  Array.from(elements).forEach((el) => {
    // Disable all form elements
    el.setAttribute('disabled', true);
  });
</script>
```

Although the `form.elements` is considered an [older API](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCollection), it's still very efficient when [working with multiple forms](https://stackoverflow.com/a/75669350/1727948)
