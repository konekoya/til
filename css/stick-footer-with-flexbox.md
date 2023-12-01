# Stick footer with Flexbox

Stick footer is a very popular way to ensure your footer stay at the very bottom of your site even when the content is not long enough. Here is a very simple and minimal implementation that I have come across today


HTML

```html
<div class="wrapper">
  <header class="page-header">This is the header</header>
  <main class="page-body">
    <p>Main page content here, add more if you want to see the footer push down.</p>
  </main>
  <footer class="page-footer">Sticky footer</footer>
</div>
```

CSS

```css
html, body {
  /* Ensure both html and body expand to full height */
  height: 100%;
}

.wrapper {
  min-height: 100%;

  /* Create the vertical layout with flex */
  display: flex;
  flex-direction: column;
}

.page-header, .page-footer {

  /* Make sure these elements won't take up spaces other than their own  */
  flex-grow: 0;
  flex-shrink: 0;
}

.page-body {

  /* Finally, the body should be able to take up as much space as it can */
  flex-grow: 1;
}
```

As you can see in the example. With just a few lines of CSS, we can create the sticky footer with flex (probably can achieve this with grid as well but fewer lines)

See [MDN docs](https://developer.mozilla.org/en-US/docs/Web/CSS/Layout_cookbook/Sticky_footers#the_recipe) for more information about this technique