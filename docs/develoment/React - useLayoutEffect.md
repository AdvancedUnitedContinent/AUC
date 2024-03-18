# useLayoutEffect

> useLayoutEffect is a version of useEffect that fires before the browser repaints the screen.

```
useLayoutEffect(setup, dependencies?)
```

### Reference

#### - useLayoutEffect(setup, dependencies?) 

- Call useLayoutEffect to perform the layout measurements before the browser repaints the screen:

```
import { useState, useRef, useLayoutEffect } from 'react';

function Tooltip() {
  const ref = useRef(null);
  const [tooltipHeight, setTooltipHeight] = useState(0);

  useLayoutEffect(() => {
    const { height } = ref.current.getBoundingClientRect();
    setTooltipHeight(height);
  }, []);
  // ...
```

#### Parameters

- setup: The function with your Effect’s logic. Your setup function may also optionally return a cleanup function. Before your component is added to the DOM, React will run your setup function. After every re-render with changed dependencies, React will first run the cleanup function (if you provided it) with the old values, and then run your setup function with the new values. Before your component is removed from the DOM, React will run your cleanup function.

- optional dependencies: The list of all reactive values referenced inside of the setup code. Reactive values include props, state, and all the variables and functions declared directly inside your component body. If your linter is configured for React, it will verify that every reactive value is correctly specified as a dependency. The list of dependencies must have a constant number of items and be written inline like [dep1, dep2, dep3]. React will compare each dependency with its previous value using the Object.is comparison. If you omit this argument, your Effect will re-run after every re-render of the component.


#### Returns

useLayoutEffect returns undefined.

#### Caveats

useLayoutEffect is a Hook, so you can only call it at the top level of your component or your own Hooks. You can’t call it inside loops or conditions. If you need that, extract a component and move the Effect there.

When Strict Mode is on, React will run one extra development-only setup+cleanup cycle before the first real setup. This is a stress-test that ensures that your cleanup logic “mirrors” your setup logic and that it stops or undoes whatever the setup is doing. If this causes a problem, implement the cleanup function.

If some of your dependencies are objects or functions defined inside the component, there is a risk that they will cause the Effect to re-run more often than needed. To fix this, remove unnecessary object and function dependencies. You can also extract state updates and non-reactive logic outside of your Effect.

Effects only run on the client. They don’t run during server rendering.

The code inside useLayoutEffect and all state updates scheduled from it block the browser from repainting the screen. When used excessively, this makes your app slow. When possible, prefer useEffect.

### Usage

> Measuring layout before the browser repaints the screen 

Most components don’t need to know their position and size on the screen to decide what to render. They only return some JSX. Then the browser calculates their layout (position and size) and repaints the screen.

Sometimes, that’s not enough. Imagine a tooltip that appears next to some element on hover. If there’s enough space, the tooltip should appear above the element, but if it doesn’t fit, it should appear below. In order to render the tooltip at the right final position, you need to know its height (i.e. whether it fits at the top).

To do this, you need to render in two passes:

Render the tooltip anywhere (even with a wrong position).
Measure its height and decide where to place the tooltip.
Render the tooltip again in the correct place.
All of this needs to happen before the browser repaints the screen. You don’t want the user to see the tooltip moving. Call useLayoutEffect to perform the layout measurements before the browser repaints the screen:

```
function Tooltip() {
  const ref = useRef(null);
  const [tooltipHeight, setTooltipHeight] = useState(0); // You don't know real height yet

  useLayoutEffect(() => {
    const { height } = ref.current.getBoundingClientRect();
    setTooltipHeight(height); // Re-render now that you know the real height
  }, []);

  // ...use tooltipHeight in the rendering logic below...
}
```

Here’s how this works step by step:

Tooltip renders with the initial tooltipHeight = 0 (so the tooltip may be wrongly positioned).
React places it in the DOM and runs the code in useLayoutEffect.
Your useLayoutEffect measures the height of the tooltip content and triggers an immediate re-render.
Tooltip renders again with the real tooltipHeight (so the tooltip is correctly positioned).
React updates it in the DOM, and the browser finally displays the tooltip.
Hover over the buttons below and see how the tooltip adjusts its position depending on whether it fits:




