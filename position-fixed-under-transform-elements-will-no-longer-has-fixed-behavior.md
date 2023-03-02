# Position fixed under transform elements will no longer has fixed behavior

When setting an HTML element with `position: fixed`, the element is remove from the normal document flow as seen in the [MDN docs](https://developer.mozilla.org/en-US/docs/Web/CSS/position):

> The element is removed from the normal document flow, and no space is created for the element in the page layout

However, if one of its ancestors has a trasform set to something other than `none`, the ancestor will be the containing block so the original fixed behavior will no longer work. This is also stated in the docs, but I just never read it 😅

> except when one of its ancestors has a transform, perspective, or filter property set to something other than none (see the CSS Transforms Spec), or the will-change property is set to transform, in which case that ancestor behaves as the containing block. (Note that there are browser inconsistencies with perspective and filter contributing to containing block formation.) Its final position is determined by the values of top, right, bottom, and left.

Note that there are also other rules that could "break" the fixed behavior

Here is a [quick example](https://codesandbox.io/s/cranky-gates-pymfb2) that demonstrate the problem. Try remove and add back the `style` tag on the `<animated.div>` to see the fixed behavior gets affected by the `transform` rule

```js
import './styles.css';
import { useSpring, animated } from '@react-spring/web';

export default function App() {
  const transitions = useSpring({
    from: {
      opacity: 0.8,
      transform: 'translateX(-80px)',
    },
    enter: {
      opacity: 1,
      transform: 'translateX(0)',
    },
    config: {
      duration: 200,
    },
  });

  return (
    <animated.div style={transitions}>
      <h1>Some very long content to be able to scroll page</h1>

      <div className="sticky">
        i'm a div that should stick on the bottom right of your screen
      </div>
    </animated.div>
  );
}
```

See also this great [SO question](https://stackoverflow.com/questions/2637058/position-fixed-doesnt-work-when-using-webkit-transform) regarding the issue
