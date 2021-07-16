<template>
  <view class="element" v-if="isFontLoaded">
    <view class="element__dot"></view>
    <text class="element__text">{{ title }}</text>
    <view class="element__dot element__dot-red" v-if="isCollapsed"></view>
    <text v-if="date" class="element__text">{{ date }}</text>
  </view>
</template>

<script>
import * as Font from "expo-font";

export default {
  name: "AppToDoListCategoryElement",
  props: {
    title: {
      required: true
    },
    date: {
      type: Object,
      required: false
    },
    isCollapsed: {
      type: Boolean,
      default: true
    },
  },
  data() {
    return {
      isFontLoaded: false
    }
  },
  async created() {
    await Font.loadAsync({
      RobotoLight: require("../node_modules/@expo-google-fonts/roboto/Roboto_300Light.ttf"),
    })
    this.isFontLoaded = true
  },
}
</script>

<style scoped>
.element {
  flex-direction: row;
  align-self: stretch;
  justify-content: flex-start;
  align-items: flex-start;
  margin-bottom: 8px;
}

.element__dot {
  width: 5px;
  height: 5px;
  border-radius: 2px;
  background-color: #8E8D8D;
  margin-right: 10px;
  margin-top: 4px;
}

.element__text {
  font-family: RobotoLight;
  line-height: 14px;
  font-size: 14px;
  color: #8E8D8D;
  margin-right: 10px;
  max-width: 50%;
}

.element__dot-red{
  background-color: #FFA7A7;
}
</style>
