<template>
  <view class="calendar__container">
    <view v-for="(item ,index) in daysOfWeek" :key="item">
      <text :class="{'calendar__element-title' : true, 'active': (index+1 === dayOfWeek)}">{{ item }}</text>
      <text :class="{'calendar__element-value' : true, 'active': (index+1 === dayOfWeek)}">{{ getNumberOfDay(index + 1) }}</text>
    </view>
  </view>
</template>

<script>

export default {
  name: "AppHeaderCalendar",
  data() {
    return {
      currentDate: new Date(),
      daysOfWeek: ["Пн", "Вт", "Ср", "Чт", "Пт", "Сб", "Вс"],
    }
  },
  computed: {
    dayOfWeek() {
      return this.currentDate.getDay() || 7
    },
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
    font-size: 18px;
    color: white;
    font-weight: 500;
}

.calendar__element-value {
    font-size: 14px;
    color: white;
    font-weight: 400;
}

.active{
    font-size: 18px;
    font-weight: 700;
}
</style>
