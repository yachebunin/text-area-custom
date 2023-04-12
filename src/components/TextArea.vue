<template>
  <div class="text-area">
    <div class="text-area__title">{{ title }}</div>
    <div class="text-area__wrapper">
      <textarea
          v-model="text"
          :placeholder="placeholder"
          :style="{width: width, height: height}"
          :class="{'text-area__input_error': getError}"
          @input="loading(true)"
          @focusin="focusArea(true)"
          @focusout="focusArea(false); loading(false)"
          class="text-area__input"
      >
      </textarea>
      <span class="text-area__label" :class="{'text-area__label_disabled': text.length || isFocusArea}">Название поля</span>
      <img v-if="isLoading" class="text-area__loader" src="../assets/earth.gif" alt="loading">
    </div>
    <div v-if="getError" class="text-area__error">Ошибка</div>
    <div class="text-area__counter">
      <span>{{ text.length }}</span> / <span>{{ maxValue }}</span>
    </div>
    <button @click="clearTextArea" class="text-area__clear">Очистить</button>
  </div>
</template>

<script>
export default {
  name: 'TextArea',
  data() {
    return {
      text: '10 symbols',
      isFocusArea: false,
      isLoading: false
    }
  },
  props: {
    placeholder: {
      type: String,
      default: ''
    },
    width: {
      type: String,
      default: '300px'
    },
    height: {
      type: String,
      default: '100px'
    },
    title: {
      type: String,
      default: 'Текст перед полем ввода: обратите внимание на prop "minValue", меньше него - ошибка'
    },
    minValue: {
      type: Number,
      default: 10
    },
    maxValue: {
      type: Number,
      default: 1000
    },
  },
  computed: {
    getError() {
      const length = this.text.length
      return length >= this.maxValue || length < this.minValue
    }
  },
  methods: {
    clearTextArea() {
      this.text = ''
    },
    focusArea(is) {
      this.isFocusArea = is
    },
    loading(is) {
      this.isLoading = is
    }
  }
}
</script>

<style lang="scss" scoped>
  .text-area {
    font-family: 'Roboto';
    &__title {
      margin-bottom: 4px;
      font-weight: 500;
      font-size: 18px;
      line-height: 24px;
      letter-spacing: 0.0015em;
      color: #303030;
    }
    &__wrapper {
      position: relative;
      max-width: max-content;
    }
    &__label {
      position: absolute;
      left: 5px;
      top: 5px;
      font-style: normal;
      font-size: 16px;
      line-height: 22px;
      letter-spacing: 0.0015em;
      color: #878F97;
      transition: all 0.3s;
      &_disabled {
        font-size: 11px;
        line-height: 12px;
        letter-spacing: 0.004em;
        color: #878F97;
      }
    }
    &__loader {
      position: absolute;
      right: 10px;
      top: 10px;
      width: 15px;
    }
    &__input {
      margin-bottom: 8px;
      padding: 22px 4px 4px;
      border-radius: 8px;
      background: #F0F0F0;
      caret-color: #00B6D0;
      border: none;
      outline: none;
      resize: none;
      &_error {
        background: #FBF0EF;
      }
    }
    &__error {
      line-height: 20px;
      letter-spacing: 0.0025em;
      color: #D6675C;
    }
    &__counter {
      font-weight: 400;
      line-height: 20px;
      letter-spacing: 0.0025em;
      color: #878F97;
    }
    &__clear {
      padding: 0px;
      line-height: 20px;
      letter-spacing: 0.0025em;
      color: #00B6D0;
      outline: none;
      border: none;
      background: transparent;
      cursor: pointer;
    }
  }
</style>
