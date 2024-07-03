  <script>
  export default {
    name: 'Form',
    props: {
      title: {
        type: String,
        required: true
      },
      button: {
        type: String,
        required: true
      },
      maxLength: {
        type: Number,
        required: true
      }
    },
    data() {
      return {
        inputValue: ''
      }
    },
    methods: {
      validateInput(event) {
        const value = event.target.value;
        const filteredValue = value.replace(/[^a-zA-Z\s]/g, '');
        const truncatedValue = filteredValue.slice(0, this.maxLength);
        this.inputValue = truncatedValue;
      },
      handleClick() {
        this.$emit('nextStage', this.inputValue);
      }
    }
  }
  </script>
<template>
    <div class="form">
      <div class="form-title">{{ title }}</div>
      <input 
        type="text" 
        class="form-input" 
        v-model="inputValue" 
        @input="validateInput"
      >
      <button :disabled="inputValue.length === 0" @click="handleClick">{{ button }}</button>
    </div>
  </template>
  

<style lang="scss">
@import '../assets/scss/global.scss';

.form {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    justify-content: center;
    margin-top: 20px;

    &-title {
        font-size: 1.5em;
        margin-bottom: 10px;
    }

    &-input {
        padding: 10px 5px;
        border: 0;
        border-radius: 5px;
        margin: 10px 0;
        text-align: center;
        color: $black;
        font-size: 16px;
    }
}
</style>
