# Create a Full Screen Background Image with Object Fit

A popular way to create a full screen background image that "cover"s and "center"s within the viewport is by using CSS's `background-image` property with `cover` (or `contain`, depending on your need) and `center` values. However, when using `<img>` tags to load images, you need to use `object-fit` to achieve a similar effect.

Here is an example of a full screen background using `background-image`:

```html
<!-- CSS -->
<style>
  .container {
    background-image: url('./home-bg.jpg');
    background-size: cover;
    background-position: center;
    width: 100vw;
    height: 100vh;
    position: absolute;
    left: 0;
    top: 0;
  }
</style>

<!-- HTML -->
<div class="container">
  Lorem, ipsum dolor sit amet consectetur adipisicing elit. Reiciendis sed
  dignissimos voluptas, incidunt, accusamus et numquam ipsam quam excepturi
  perspiciatis rerum ipsum harum, quidem beatae velit magnam officia? Explicabo,
  numquam.
</div>
```

With using `<img>` tags, you can achieve a similar effect by using `object-fit` property:

```html
<!-- CSS -->
<style>
  img {
    width: 100vw;
    height: 100vh;
    position: absolute;
    left: 0;
    top: 0;
    object-fit: cover;
  }
</style>

<!-- HTML -->
<img src="./home-bg.jpg" alt="My Beautiful Home Background" />
```

For more information on this topic, check out this [SackOverflow answer](https://stackoverflow.com/a/26967278/1727948), which includes another technique for using CSS to replace an `<img>` with a background image.
