## react-native-modal-datetime-picker

> 사용 목적 : 달력에서 날짜를 선택하도록 하기 위하여 사용

* 설치 : 
```npm i react-native-modal-datetime-picker```

### Setup

```
npx expo install react-native-modal-datetime-picker @react-native-community/datetimepicker
```
> 설정 : app.json 
```
{
  "expo": {
    "userInterfaceStyle": "automatic"
  }
}
```

## Useage
```
import React, { useState } from "react";
import { Button, View } from "react-native";
import DateTimePickerModal from "react-native-modal-datetime-picker";

const Example = () => {
  const [isDatePickerVisible, setDatePickerVisibility] = useState(false);

  const showDatePicker = () => {
    setDatePickerVisibility(true);
  };

  const hideDatePicker = () => {
    setDatePickerVisibility(false);
  };

  const handleConfirm = (date) => {
    console.warn("A date has been picked: ", date);
    hideDatePicker();
  };

  return (
    <View>
      <Button title="Show Date Picker" onPress={showDatePicker} />
      <DateTimePickerModal
        isVisible={isDatePickerVisible}
        mode="date"
        onConfirm={handleConfirm}
        onCancel={hideDatePicker}
      />
    </View>
  );
};

export default Example;
```