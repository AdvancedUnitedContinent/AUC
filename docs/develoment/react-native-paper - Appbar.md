## Appbar

A component to display action items in a bar. It can be placed at the top or bottom. The top bar usually contains the screen title, controls such as navigation buttons, menu button etc. The bottom bar usually provides access to a drawer and up to four actions.

By default Appbar uses primary color as a background, in dark theme with adaptive mode it will use surface colour instead. See Dark Theme for more informations


### Usage

```
import * as React from 'react';
import { Appbar } from 'react-native-paper';

const MyComponent = () => (
  <Appbar.Header>
    <Appbar.BackAction onPress={() => {}} />
    <Appbar.Content title="Title" />
    <Appbar.Action icon="calendar" onPress={() => {}} />
    <Appbar.Action icon="magnify" onPress={() => {}} />
  </Appbar.Header>
);

export default MyComponent;
```


[Docs-link](https://callstack.github.io/react-native-paper/docs/components/Appbar/#usage)