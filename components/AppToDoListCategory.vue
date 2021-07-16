<template>
  <Pressable class="category__wrapper" v-if="isFontLoaded" :onPress="onPressArrowIcon">
    <view class="category__wrapper__row-first">
      <view class="category__title__wrapper">
        <text class="category__title" :numberOfLines="isCollapsed ? 1 : 0">
          <slot>
            Категория
          </slot>
        </text>
        <image
            v-if="isManyToDos"
            :source="require('../assets/icons/arrow-down.png')"
            :class="{'arrow-down-icon' : true, 'collapsed' : isCollapsed, 'not-collapsed' : !isCollapsed}"
        />
      </view>
      <AppButton is-black is-not-margin/>
    </view>
    <view :class="{'category__wrapper__row-second': true, 'row_collapsed' : isCollapsed}">
      <AppToDoListCategoryElement
          v-for="todo in todos"
          :key="todo.title"
          :title="todo.title"
          :isCollapsed="isCollapsed"
      />
    </view>
  </Pressable>
</template>

<script>
import * as Font from "expo-font";
import AppButton from "./AppButton";
import AppToDoListCategoryElement from "./AppToDoListCategoryElement";

export default {
  name: "AppToDoCategory",
  components: {AppButton, AppToDoListCategoryElement},
  props: {
    isManyToDos: {
      type: Boolean,
      required: false
    },
    todos: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      isCollapsed: true,
      isFontLoaded: false
    }
  },
  async created() {
    await Font.loadAsync({
      //RobotoLight: require("../node_modules/@expo-google-fonts/roboto/Roboto_300Light.ttf"),
      RobotoRegular: require("../node_modules/@expo-google-fonts/roboto/Roboto_400Regular.ttf")
    })
    this.isFontLoaded = true
  },
  methods: {
    onPressArrowIcon() {
      this.isCollapsed = !this.isCollapsed
    }
  }
}
</script>

<style scoped>
.category__wrapper {
  align-self: stretch;
  border-radius: 30px;
  background-color: hsl(100, 100%, 100%);
  padding-left: 30px;
  padding-right: 30px;
  padding-top: 20px;
  padding-bottom: 20px;
  elevation: 1;
  margin-bottom: 25px;
}

.category__wrapper__row-first {
  align-items: center;
  flex-direction: row;
  justify-content: space-between;
}

.category__title__wrapper {
  flex-direction: row;
  align-items: center;
  justify-content: flex-start;
  max-width: 80%;
}

.category__title {
  font-family: RobotoRegular;
  font-size: 18px;
  line-height: 18px;
  margin-right: 10px;
  max-width: 100%;
}

.arrow-down-icon {
  width: 10px;
  height: 5px;
}

.collapsed {
  transform: rotateX(0);
}

.not-collapsed {
  transform: rotateX(180deg);
}

.category__wrapper__row-second {

}

.row_collapsed {
  max-height: 15px;
  overflow: hidden;
}

</style>
