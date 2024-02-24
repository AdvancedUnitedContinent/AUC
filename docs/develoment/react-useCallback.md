## useCallback

- useCallback is a React Hook that lets you cache a function definition between re-renders.



```
const cachedFn = useCallback(fn, dependencies)
```

- Reference
    - useCallback(fn, dependencies)

- Usage
Skipping re-rendering of components
    - Updating state from a memoized callback
    - Preventing an Effect from firing too often
    - Optimizing a custom Hook

- Troubleshooting
    - Every time my component renders, useCallback returns a different function
    - I need to call useCallback for each list item in a loop, but it’s not allowed


### Reference 
useCallback(fn, dependencies) 
Call useCallback at the top level of your component to cache a function definition between re-renders:


```
import { useCallback } from 'react';

export default function ProductPage({ productId, referrer, theme }) {
  const handleSubmit = useCallback((orderDetails) => {
    post('/product/' + productId + '/buy', {
      referrer,
      orderDetails,
    });
  }, [productId, referrer]);
```