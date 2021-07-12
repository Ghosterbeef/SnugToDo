<template>
  <view class="header__container">
    <status-bar
      background-color="#FFA7A7"
      bar-style="light-content"
    />
    <text class="header__title raleway_bold">Мои задачи</text>
    <AppHeaderCalendar/>
  </view>
</template>

<script>
import AppHeaderCalendar from "./AppHeaderCalendar"

export default {
  name: "AppHeader",
  components: {AppHeaderCalendar},

}
</script>

<style>
.header__container {
    width: 100%;
    padding-top: 50px;
    padding-left: 20px;
}

.header__title {
    font-size: 36px;
    color: white;
}

</style>
