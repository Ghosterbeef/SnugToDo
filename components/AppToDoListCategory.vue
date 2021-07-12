<template>
  <Pressable class="category__wrapper">
    <view class="category__wrapper__row-first">
      <text class="category__title">
        <slot>
          Категория
        </slot>
      </text>
    </view>
    <view class="category__wrapper__row-second">
      <slot name="todos">

      </slot>
    </view>
  </Pressable>
</template>

<script>
export default {
  name: "AppToDoCategory"
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
}

.category__title {
  font-size: 18px;
  font-weight: 400;
}
</style>
