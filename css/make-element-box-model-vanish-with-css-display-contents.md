# Make Element Box model vanish with CSS display contents 

`display: contents` is a new addition to the CSS world of `display` property. When applied to a parent element, it significantly alters the box model, resulting in the background, border, and padding not being rendered. This effectively makes the element's box "vanish" (or disappear) and its children elements are instead treated as direct children of the grandparent element for layout purposes.

Here's an illustrative example:

```html
<div class="parent">
  <div>Item one</div>
  <div>Item two</div>
  <div>Item three</div>
</div>
```

And with this layout, we have some CSS like below:

```css
.parent {
  display: flex;
  justify-content: space-between;
}
```

This layout looks pretty good. You were satisfied with the layout and considered it done for the day. But imagine like some days later, you PM asks you to add a new feature and somehow that you need to wrap the items (one, two and three) in a new div. Oops, this breaks the layout because these children elements are no longer the direct child of the `.parent` class. No worried, `display: contents` comes to the rescue

Just add it to the new div and ta-da! It works again :)

For resource about `display: contents`:

- [Get Ready for `display: contents;`](https://css-tricks.com/get-ready-for-display-contents/)
- [But doesn't display: contents in effect simulate the contents as belonging to the grandparent element?](https://stackoverflow.com/a/73008545/1727948)