### Introduction


Gesture Handler aims to replace React Native's built in touch system called Gesture Responder System.

The motivation for building this library was to address the performance limitations of React Native's Gesture Responder System and to provide more control over the built-in native components that can handle gestures. We recommend this talk by Krzysztof Magiera in which he explains issues with the responder system.



### Step 1
First let's define styles we will need to make the app:

```
import { StyleSheet } from 'react-native';

const styles = StyleSheet.create({
  ball: {
    width: 100,
    height: 100,
    borderRadius: 100,
    backgroundColor: 'blue',
    alignSelf: 'center',
  },
});
```

### 