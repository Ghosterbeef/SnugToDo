<template>
  <Pressable :class="{'add-category__btn': true,
             'black': isBlack,
             'centered': isCentered,
             'stretched' : isStretched,
             'bigger-br' : isBiggerBr,
             'small-margin' : isSmallMargin,
             'not-margin' : isNotMargin,
             }"
             :onPress="onPress"
             v-if="isFontLoaded">
    <view>
      <text :class="{'btn__text': true,'black': isBlack, 'text-contained' : isTextContained}">
        <slot>
          +
        </slot>
      </text>
    </view>
  </Pressable>
</template>

<script>
import * as Font from "expo-font";

export default {
  name: "AppButton",
  props: {
    isCentered: {
      type: Boolean,
      default: false
    },
    isStretched: {
      type: Boolean,
      default: false
    },
    isTextContained: {
      type: Boolean,
      default: false
    },
    isBiggerBr: {
      type: Boolean,
      default: false
    },
    isSmallMargin: {
      type: Boolean,
      default: false
    },
    isNotMargin: {
      type: Boolean,
      default: false
    },
    isBlack: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      isFontLoaded: false
    }
  },
  async created() {
    await Font.loadAsync({
      RobotoMedium: require("../node_modules/@expo-google-fonts/roboto/Roboto_500Medium.ttf")
    })
    this.isFontLoaded = true
  },
  methods: {
    onPress() {
      this.$emit("onPress")
    }
  }
}
</script>

<style scoped>
.add-category__btn {
  background-color: #FFA7A7;
  border-radius: 10px;
  width: 41px;
  height: 41px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 30px;
  margin-top: 30px;
  elevation: 5;
}

.centered {
  align-self: center;
}

.stretched {
  width: 100%;
}

.bigger-br {
  border-radius: 30px;
}

.small-margin {
  margin-bottom: 20px;
  margin-top: 20px;
}

.btn__text {
  color: white;
  font-size: 30px;
  font-weight: 400;
}

.text-contained {
  font-size: 18px;
  font-family: RobotoMedium;
}

.black{
  background-color: transparent;
  elevation: 0;
  color: black;
}

.not-margin{
  margin-top: 0;
  margin-bottom: 0;
}

</style>
