# useRef

```
const ref = useRef(initialValue)
```

## Reference 
```
import { useRef } from 'react';

function MyComponent() {
  const intervalRef = useRef(0);
  const inputRef = useRef(null);
```

## Usage

```
import { useRef } from 'react';

function Stopwatch() {
  const intervalRef = useRef(0);
```

```
function handleStartClick() {
  const intervalId = setInterval(() => {
    // ...
  }, 1000);
  intervalRef.current = intervalId;
}
```

```
function handleStopClick() {
  const intervalId = intervalRef.current;
  clearInterval(intervalId);
}
```