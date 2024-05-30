# Expo Updates


A library that allows programmatically controlling and responding to new updates made available to your app.

The expo-updates library allows you to programmatically control and respond to new updates made available to your app.


```
import { View, Button } from 'react-native';
import * as Updates from 'expo-updates';

function App() {
  async function onFetchUpdateAsync() {
    try {
      const update = await Updates.checkForUpdateAsync();

      if (update.isAvailable) {
        await Updates.fetchUpdateAsync();
        await Updates.reloadAsync();
      }
    } catch (error) {
      // You can also add an alert() to see the error message in case of an error when fetching updates.
      alert(`Error fetching latest Expo update: ${error}`);
    }
  }

  return (
    <View>
      <Button title="Fetch update" onPress={onFetchUpdateAsync} />
    </View>
  );
}

```