<template>
  <view class="app__container">
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
</style>
