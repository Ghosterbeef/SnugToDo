<template>
  <view class="todo__container" v-if="isFontLoaded">
    <Modal animationType="slide"
           :transparent="true"
           :hardwareAccelerated="true"
           :onRequestClose="onPressAddToDoButton"
           v-if="isAddToDoShow"
    >
      <view class="modal__empty"></view>
      <view class="modal__inner">
        <view class="modal__inner-content__wrapper">
          <view class="modal__inner-content__wrapper__form-group">
            <text class="modal__inner-content__category__name">Название категории</text>
            <text-input
                class="modal__inner-content__category__name__input"
                v-model="categoryNameInput"
                placeholder="Введите название"
            />
            <AppButton @onPress="onPressAddCategoryButton"
                       is-centered
                       is-stretched
                       is-text-contained
                       is-bigger-br
                       is-small-margin
            >
              Создать категорию
            </AppButton>
          </view>
          <view class="modal__inner-content__cancel-btn__wrapper">
            <AppButton @onPress="onPressAddToDoButton" is-centered>
              &times;
            </AppButton>
          </view>
        </view>
      </view>
    </Modal>
    <view class="todo__scroll__wrapper" v-if="!isAddToDoShow">
      <scroll-view class="todo__scroll">
        <view class="todos__container">
          <AppToDoCategory v-for="category in categories"
                           :key="category.title"
                           :isManyToDos="category.todos.length>1"
                           :todos="category.todos"
          >
            <text>{{ category.title }}</text>
          </AppToDoCategory>
          <AppButton @onPress="onPressAddToDoButton"/>
        </view>
      </scroll-view>
    </view>
  </view>
</template>

<script>

import AppButton from "./AppButton";
import AppToDoCategory from "./AppToDoListCategory";
import * as Font from "expo-font";
import AppToDoCategoryElement from "./AppToDoListCategoryElement";

export default {
  name: "AppToDoList",
  components: {AppToDoCategoryElement, AppToDoCategory, AppButton},
  data() {
    return {
      isAddToDoShow: false,
      categoryNameInput: "",
      isInputError: false,
      isFontLoaded: false,
      categories: []
    }
  },
  async created() {
    await Font.loadAsync({
      RobotoLight: require("../node_modules/@expo-google-fonts/roboto/Roboto_300Light.ttf"),
      RobotoRegular: require("../node_modules/@expo-google-fonts/roboto/Roboto_400Regular.ttf"),
    })
    this.isFontLoaded = true
  },
  methods: {
    onPressAddToDoButton() {
      this.isInputError = false
      this.isAddToDoShow = !this.isAddToDoShow
    },
    onPressAddCategoryButton() {
      if (!this.categoryNameInput) {
        this.isInputError = true
        return
      }
      this.categories.push(
          {
            title: this.categoryNameInput,
            todos: [{title: "Выпить теблетку от головы"}, {title: "Принять 2 таблетки черники форте"}]
          }
      )
      this.categoryNameInput = ''
      this.isInputError = false
      this.isAddToDoShow = !this.isAddToDoShow
    }
  }
}
</script>

<style scoped>
.todo__container {
  align-self: stretch;
  flex-basis: auto;
  flex-grow: 1;
}

.modal__empty {
  flex-basis: 182px;
}

.modal__inner {
  flex-grow: 1;
  background-color: rgba(229, 229, 229, 0.6);
  padding-top: 35px;
  padding-left: 35px;
  padding-right: 35px;
  align-items: center;
  border-top-left-radius: 50px;
  border-top-right-radius: 50px;
}

.modal__inner-content__wrapper {
  flex: 1;
  align-self: stretch;
  align-items: flex-start;
}

.modal__inner-content__wrapper__form-group {
  align-self: stretch;
}

.modal__inner-content__category__name {
  color: #3E3E3E;
  font-family: RobotoMedium;
  font-size: 18px;
  padding-left: 20px;
}

.modal__inner-content__category__name__input {
  align-self: stretch;
  background-color: white;
  border-radius: 30px;
  padding-top: 10px;
  padding-bottom: 10px;
  padding-left: 20px;
  padding-right: 20px;
  margin-top: 15px;
}

.modal__inner-content__cancel-btn__wrapper {
  flex-grow: 1;
  justify-content: flex-end;
  align-self: stretch;
}

.todo__scroll__wrapper {
  margin-top: 20px;
  align-items: stretch;
  flex: 1;
  background-color: rgba(229, 229, 229, 0.6);
  border-top-left-radius: 50px;
  border-top-right-radius: 50px;
}

.todos__container {
  width: 100%;
  align-items: center;
  padding: 30px;
}

</style>
