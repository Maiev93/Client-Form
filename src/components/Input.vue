<template>
  <div class="input">
    <p class="input__text">{{ text }}</p>
    <input class="input__input" :type="type" />
  </div>
</template>

<script>
export default {
  name: "Input",
  props: {
    type: String,
    text: String,
    required: Boolean,
    pattern: String,
    maxLength: String,
  },
};
</script>

<style lang="scss">
.input {
  display: flex;
  justify-content: space-between;
  margin: 2%;
  position: relative;
  &__input {
    border-radius: 15px;
    box-shadow: 0px 0px 2px 1px #646d8f;
    outline: none;
    border: none;
    width: 300px;
  }

  &__text {
    margin: 3%;
  }
}
</style>
