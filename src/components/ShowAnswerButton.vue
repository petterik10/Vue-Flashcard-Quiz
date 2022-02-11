<template>
  <div @click="$emit('toggle-showAnswer')">
    <button class="answer-button">
      {{ btnText }}
    </button>
  </div>
</template>

<script>
export default {
  name: "ShowAnswerButton",
  props: {
    btnText: String,
  },
 
};
</script>

<style lang="scss" scoped>
.answer-button {
  background-color: rgb(65, 65, 131);
  cursor: pointer;
  position: absolute;
  bottom: 0px;
  left: 0;
  color: white;
  width: 236px;
  height: 40px;
  border: none;
  outline: none;
}
</style>