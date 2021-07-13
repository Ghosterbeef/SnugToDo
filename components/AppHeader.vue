<template>
  <view class="header__container" v-if="isFontLoaded">
    <status-bar
        background-color="#FFA7A7"
        bar-style="light-content"
    />
    <text class="header__title">Мои задачи</text>
    <AppHeaderCalendar/>
  </view>
</template>

<script>
import AppHeaderCalendar from "./AppHeaderCalendar"
import * as Font from "expo-font";

export default {
  name: "AppHeader",
  components: {AppHeaderCalendar},
  data() {
    return {
      isFontLoaded: false
    }
  },
  async created() {
    await Font.loadAsync({
      RalewayBold: require("../node_modules/@expo-google-fonts/raleway/Raleway_700Bold.ttf"),
      // RobotoLight: require("./node_modules/@expo-google-fonts/roboto/Roboto_300Light.ttf"),
      // RobotoRegular: require("./node_modules/@expo-google-fonts/roboto/Roboto_400Regular.ttf"),
      // RobotoMedium: require("./node_modules/@expo-google-fonts/roboto/Roboto_500Medium.ttf"),
    })
    this.isFontLoaded = true
  }

}
</script>

<style>
.header__container {
  width: 100%;
  padding-top: 50px;
  padding-left: 20px;
}

.header__title {
  font-family: RalewayBold;
  font-size: 36px;
  color: white;
}

</style>
