## react-native-popover-view

> npm i react-native-popover-view

Table of Contents
- Features
- Installation
- Usage
- Props
- Usage with Safe Area Context
- Troubleshooting
- Upgrading
- Contributing
- Credits

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

```
import React, { useState, useEffect } from 'react';
import Popover from 'react-native-popover-view';

function App() {
  const [showPopover, setShowPopover] = useState(false);

  useEffect(() => {
    setTimeout(() => setShowPopover(false), 2000);
  }, []);

  return (
    <Popover
      isVisible={showPopover}
      onRequestClose={() => setShowPopover(false)}
      from={(
        <TouchableOpacity onPress={() => setShowPopover(true)}>
          <Text>Press here to open popover!</Text>
        </TouchableOpacity>
      )}>
      <Text>This popover will be dismissed automatically after 2 seconds</Text>
    </Popover>
  );
}
```