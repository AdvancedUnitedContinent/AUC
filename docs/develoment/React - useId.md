# useId

- useId is a React Hook for generating unique IDs that can be passed to accessibility attributes.

## Reference

- Call useId at the top level of your component to generate a unique ID:


```
import { useId } from 'react';

function PasswordField() {
  const passwordHintId = useId();
  // ...

```



- Parameters 
useId does not take any parameters.

- Returns 
useId returns a unique ID string associated with this particular useId call in this particular component.

- Caveats 
useId is a Hook, so you can only call it at the top level of your component or your own Hooks. You can’t call it inside loops or conditions. If you need that, extract a new component and move the state into it.

useId should not be used to generate keys in a list. Keys should be generated from your data.


```
import { useId } from 'react';

function PasswordField() {
  const passwordHintId = useId();
  return (
    <>
      <label>
        Password:
        <input
          type="password"
          aria-describedby={passwordHintId}
        />
      </label>
      <p id={passwordHintId}>
        The password should contain at least 18 characters
      </p>
    </>
  );
}

export default function App() {
  return (
    <>
      <h2>Choose password</h2>
      <PasswordField />
      <h2>Confirm password</h2>
      <PasswordField />
    </>
  );
}

```
