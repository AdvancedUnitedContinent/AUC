# MobX + React Integration


- How to use:

```
import { observer } from "mobx-react-lite" // 또는 "mobx-react".

const MyComponent = observer(props => ReactElement)
```

MobX works independently of React, but is typically used in conjunction with React. We've already identified the most important part of integration in MobX's point: the observer HoC, which can wrap around React components.

The observer is provided by a separate React binding package selected during installation; the example below will use a lighter mobx-react-lite package.




The observer HoC automatically subscribes to React components to all of the observables used during rendering. As a result, if the relevant observable changes, the components are automatically re-rendered. In addition, components are not re-rendered if there are no relevant changes. Thus, an observable that can be accessed from a component but is not actually read is not re-rendered.

This logic optimizes the MobX application immediately and eliminates the need to write additional code to prevent excessive rendering.

For an observer to work, it doesn't matter how the observable arrives at the component, it just needs to be read. Deep reading of the observable works well, and complex representations work well, like todos[0].author.displayName. This logic makes the subscription mechanism much more accurate and efficient than other frameworks (selectors) that need to explicitly declare or pre-calculate data dependencies.