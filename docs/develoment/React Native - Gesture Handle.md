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

### Step 2
Then we can start writing our Ball component:

```
import { GestureDetector } from 'react-native-gesture-handler';
import Animated from 'react-native-reanimated';

function Ball() {
  return (
    <GestureDetector>
      <Animated.View style={[styles.ball]} />
    </GestureDetector>
  );
}
```


### Step 3
We also need to define shared values to keep track of the ball position and create animated styles in order to be able to position the ball on the screen:

```
import {
  useSharedValue,
  useAnimatedStyle,
  withSpring,
} from 'react-native-reanimated';

function App() {
  const isPressed = useSharedValue(false);
  const offset = useSharedValue({ x: 0, y: 0 });

  const animatedStyles = useAnimatedStyle(() => {
    return {
      transform: [
        { translateX: offset.value.x },
        { translateY: offset.value.y },
        { scale: withSpring(isPressed.value ? 1.2 : 1) },
      ],
      backgroundColor: isPressed.value ? 'yellow' : 'blue',
    };
  });

  // ...
}
```


### Step 4
And add it to the ball's styles:

```
// ...
return (
  <GestureDetector>
    <Animated.View style={[styles.ball, animatedStyles]} />
  </GestureDetector>
);
// ...
```


### Step 5
The only thing left is to define the pan gesture and assign it to the detector:

```
import { Gesture } from 'react-native-gesture-handler';

function App() {
  // ...
  const start = useSharedValue({ x: 0, y: 0 });
  const gesture = Gesture.Pan()
    .onBegin(() => {
      isPressed.value = true;
    })
    .onUpdate((e) => {
      offset.value = {
        x: e.translationX + start.value.x,
        y: e.translationY + start.value.y,
      };
    })
    .onEnd(() => {
      start.value = {
        x: offset.value.x,
        y: offset.value.y,
      };
    })
    .onFinalize(() => {
      isPressed.value = false;
    });
  // ...
}
```