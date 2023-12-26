## react-native-popover-view

> npm i react-native-popover-view


### Usage

```
import React from 'react';
import Popover from 'react-native-popover-view';

function App() {
  return (
    <Popover
      from={(
        <TouchableOpacity>
          <Text>Press here to open popover!</Text>
        </TouchableOpacity>
      )}>
      <Text>This is the contents of the popover</Text>
    </Popover>
  );
}
```

```
import React from 'react';
import Popover from 'react-native-popover-view';

function App() {
  return (
    <Popover
      from={(sourceRef, showPopover) => (
        <View>
          <TouchableOpacity onLongPress={showPopover}>
            <Text ref={sourceRef}>Press here to open popover!</Text>
          </TouchableOpacity>
        </View>
      )}>
      <Text>This is the contents of the popover</Text>
    </Popover>
  );
}
```