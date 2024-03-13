# AppState

AppState can tell you if the app is in the foreground or background, and notify you when the state changes.

AppState is frequently used to determine the intent and proper behavior when handling push notifications.


### App States

- active - The app is running in the foreground
- background - The app is running in the background. The user is either:
- - in another app
- - on the home screen
- - [Android] on another Activity (even if it was launched by your app)
- [iOS] inactive - This is a state that occurs when transitioning between foreground & background, and during periods of inactivity such as entering the multitasking view, opening the Notification Center or in the event of an incoming call.


## Basic Usage

To see the current state, you can check AppState.currentState, which will be kept up-to-date. However, currentState will be null at launch while AppState retrieves it over the bridge.

```
import React, {useRef, useState, useEffect} from 'react';
import {AppState, StyleSheet, Text, View} from 'react-native';

const AppStateExample = () => {
  const appState = useRef(AppState.currentState);
  const [appStateVisible, setAppStateVisible] = useState(appState.current);

  useEffect(() => {
    const subscription = AppState.addEventListener('change', nextAppState => {
      if (
        appState.current.match(/inactive|background/) &&
        nextAppState === 'active'
      ) {
        console.log('App has come to the foreground!');
      }

      appState.current = nextAppState;
      setAppStateVisible(appState.current);
      console.log('AppState', appState.current);
    });

    return () => {
      subscription.remove();
    };
  }, []);

  return (
    <View style={styles.container}>
      <Text>Current state is: {appStateVisible}</Text>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
});

export default AppStateExample;
```

This example will only ever appear to say "Current state is: active" because the app is only visible to the user when in the active state, and the null state will happen only momentarily. If you want to experiment with the code we recommend to use your own device instead of embedded preview.

