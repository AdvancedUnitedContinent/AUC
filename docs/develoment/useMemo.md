## useMemo

- useMemo is a React Hook that lets you cache the result of a calculation between re-renders.


```
const cachedValue = useMemo(calculateValue, dependencies)
```

## Reference 

>useMemo(calculateValue, dependencies) 

- Call useMemo at the top level of your component to cache a calculation between re-renders:

```
import { useMemo } from 'react';

function TodoList({ todos, tab }) {
  const visibleTodos = useMemo(
    () => filterTodos(todos, tab),
    [todos, tab]
  );
  // ...
}
```
