<template>
  <view class="calendar__container" v-if="isFontLoaded">
    <view v-for="(item ,index) in daysOfWeek" :key="item">
      <text :class="{'calendar__element-title' : true, 'active': (index+1 === dayOfWeek)}">{{ item }}</text>
      <text :class="{'calendar__element-value' : true, 'active': (index+1 === dayOfWeek)}">{{
          getNumberOfDay(index + 1)
        }}
      </text>
    </view>
  </view>
</template>

<script>

import * as Font from "expo-font";

export default {
  name: "AppHeaderCalendar",
  data() {
    return {
      currentDate: new Date(),
      daysOfWeek: ["Пн", "Вт", "Ср", "Чт", "Пт", "Сб", "Вс"],
      isFontLoaded: false
    }
  },
  computed: {
    dayOfWeek() {
      return this.currentDate.getDay() || 7
    },
  },
  async created() {
    await Font.loadAsync({
      RobotoLight: require("../node_modules/@expo-google-fonts/roboto/Roboto_300Light.ttf"),
      RobotoRegular: require("../node_modules/@expo-google-fonts/roboto/Roboto_400Regular.ttf"),
      RobotoBold: require("../node_modules/@expo-google-fonts/roboto/Roboto_700Bold.ttf")
    })
    this.isFontLoaded = true
  },
  methods: {
    getNumberOfDay(index) {
      if (this.currentDate.getDate() + (index - (this.currentDate.getDay() || 7)) >= 1)
        return this.currentDate.getDate() + (index - (this.currentDate.getDay() || 7))

      //let tempDate = new Date(this.currentDate.getFullYear(), this.currentMonth)
      return new Date(this.currentDate.getFullYear(), this.currentDate.getMonth()).getUTCDate() + (this.currentDate.getDate() + (index - (this.currentDate.getDay() || 7)))
    }
  }
}
</script>

<style scoped>
.calendar__container {
  width: 100%;
  flex-direction: row;
  justify-content: space-between;
  padding-top: 15px;
  padding-right: 15px;
}

.calendar__element-title {
  font-size: 14px;
  color: white;
  font-family: RobotoLight;
}

.calendar__element-value {
  font-family:RobotoLight;
  font-size: 14px;
  color: white;
}

.active {
  font-family: RobotoBold;
  font-size: 14px;
}
</style>
