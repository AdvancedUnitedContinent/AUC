React-native allows us to easily create beautiful animations easily using the Animated class. However, unless we specify ‘useNativeDriver’ when starting our animations, all the work is done on the JS thread.

This can cause frame drops in our applications. ‘useNativeDriver’ fixes this by passing all the information about our animations to the UI thread when it starts, meaning that the bridge is no longer needed during the course of the animation. In short, ‘useNativeDriver’ makes our animations run faster.

More on this in the official docs: https://facebook.github.io/react-native/blog/2017/02/14/using-native-driver-for-animated

The drawback of using ‘useNativeDriver’, is that it only supports things like transform and opacity. For example, we cannot use the native driver on an Animated.Value that is used directly on the “width” style of a view.

In this article, I will discuss a few tips and tricks for making use of the native driver on common animations.

>

Animating colors
Let’s say we have a view that should change from red to green. Our first instinct is to animate the RGB values.

```
import React, {Component} from 'react';
import {StyleSheet, View, Animated} from 'react-native';

class App extends Component {

    animatedValue = new Animated.Value(0);

    componentDidMount() {
        Animated.timing(this.animatedValue,
            {
                toValue: 1,
                duration: 1000,
            }).start();
    }

    render() {
        return (
            <View style={styles.container}>
                <Animated.View style={[styles.square, {
                    backgroundColor: this.animatedValue.interpolate(
                        {
                            inputRange: [0, 1],
                            outputRange: [
                                'rgba(255, 0, 0, 1)',
                                'rgba(0, 255, 0, 1)'
                            ]
                        })
                }]}/>
            </View>
        );
    }
}

const styles = StyleSheet.create({
    container: {
        flex: 1,
        justifyContent: 'center',
        alignItems: 'center',
    },
    square: {
        position: 'absolute',
        width: 200,
        height: 200,
        backgroundColor: 'green',
    },
});

export default App;
```


Above, we have defined an animated view. This views backgroundColor will animate from red to green over the course of 1 second using our animatedValue we set up.

This is fine, but wait, we’re not using ‘useNativeDriver’. This means if our app is doing a lot of work, we are more likely to lose frames when playing this animation as it is on the JS thread. Let’s fix this by making it use the native driver.

First we need to add “useNativeDriver: true” to our Animated.timing config. However, the backgroundColor style is not supported by the native driver.

So let’s use the opacity style instead.


If we have a red square on top of a green square, and we fade out our red square over time, we can have the same effect as our above example.

```
import React, {Component} from 'react';
import {StyleSheet, View, Animated} from 'react-native';

class App extends Component {

    animatedValue = new Animated.Value(0);

    componentDidMount() {
        Animated.timing(this.animatedValue,
            {
                toValue: 1,
                duration: 1000,
                useNativeDriver: true
            }).start();
    }

    render() {
        return (
            <View style={styles.container}>
                <View style={styles.squareBG}/>
                <Animated.View style={[styles.square, {opacity: this.animatedValue}]}/>
            </View>
        );
    }
}

const styles = StyleSheet.create({
    container: {
        flex: 1,
        justifyContent: 'center',
        alignItems: 'center',
    },
    squareBG: {
        width: 200,
        height: 200,
        backgroundColor: 'green',
    },
    square: {
        position: 'absolute',
        width: 200,
        height: 200,
        backgroundColor: 'red',
    },
});

export default App;
```


