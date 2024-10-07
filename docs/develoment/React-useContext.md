## useContext
- useContext is a React Hook that lets you read and subscribe to context from your component.

```const value = useContext(SomeContext)```


## Reference 
- useContext(SomeContext) 
Call useContext at the top level of your component to read and subscribe to context.

```
import { useContext } from 'react';

function MyComponent() {
  const theme = useContext(ThemeContext);
  // ...
```
