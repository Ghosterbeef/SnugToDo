<template>
  <view class="app__container" v-if="isFontLoaded">
    <AppHeader/>
    <AppToDoList/>
  </view>
</template>

<script>
import AppHeader from "./components/AppHeader";
import AppToDoList from "./components/AppToDoList";
import * as Font from "expo-font";

// import * as Notifications from 'expo-notifications';
// // First, set the handler that will cause the notification
// // to show the alert
// Notifications.setNotificationHandler({
//   handleNotification: async () => ({
//     shouldShowAlert: true,
//     shouldPlaySound: false,
//     shouldSetBadge: false,
//   }),
// });
// // Second, call the method
// Notifications.scheduleNotificationAsync({
//   content: {
//     title: 'Look at that notification',
//     body: "I'm so proud of myself!",
//   },
//   trigger: {
//     seconds: 10,
//   },
// });
// Notifications.cancelAllScheduledNotificationsAsync()

export default {
  components: {AppToDoList, AppHeader},
  data(){
    return{
      isFontLoaded: false
    }
  },
  async created(){
    await Font.loadAsync({
      RalewayBold: require("../node_modules/@expo-google-fonts/raleway/Raleway_700Bold.ttf"),
      RobotoLight: require("../node_modules/@expo-google-fonts/roboto/Roboto_300Light.ttf"),
      RobotoRegular: require("../node_modules/@expo-google-fonts/roboto/Roboto_400Regular.ttf"),
      RobotoMedium: require("../node_modules/@expo-google-fonts/roboto/Roboto_500Medium.ttf"),
    }).then(this.isFontLoaded = true)
  }
}
</script>

<style>
.app__container {
    background-color: #FFA7A7;
    align-items: center;
    flex: 1;
    position: relative;
}

.text-color-primary {
    color: purple;
}

.raleway-bold{
    font-family: RalewayBold;
}

.roboto_light{
    font-family: RobotoLight;
}

.roboto_regular{
    font-family: RobotoRegular;
}

.roboto_medium{
    font-family: RobotoMedium;
}
</style>
