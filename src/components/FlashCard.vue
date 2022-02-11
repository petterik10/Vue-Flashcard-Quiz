<template>
  <div class="card">
    <p class="question">{{ flashcard.question }}</p>

    <div class="flascard-options" v-if="!showAnswer">
      <div
        class="flascard-option"
        :key="option"
        v-for="(option, index) in flashcard.options"
      >
        <span> {{ index + 1 }} </span>
        {{ option }}
      </div>
    </div>
    <div v-else class="answer">
      {{ flashcard.answer }}
    </div>
    <ShowAnswerButton
      :btnText="showAnswer ? 'Show options' : 'Show correct answer'"
      @toggle-showAnswer="showAnswer = !showAnswer"
    />
  </div>
</template>

<script>
import ShowAnswerButton from "../components/ShowAnswerButton.vue";
export default {
  name: "FlashCard",
  components: { ShowAnswerButton },
  props: {
    flashcard: Object,
  },
  data() {
    return {
      showAnswer: false,
    };
  },
};
</script>

<style lang="scss" scoped>
.card {
  background-color: #faf9f9;
  perspective: 1000px;
  border-radius: 7px;
  border: 2px solid black;
  box-shadow: 0 2px 5px rgb(102, 97, 97);
  padding: 0.625em;
  width: 240px;
  height: 240px;
  margin: 1em;
  margin-left: 1.25em;
  justify-content: center;
  align-items: center;
  font-size: 0.975rem;
}

.flascard-options {
  margin-top: 0.8em;
}

.flascard-option {
  margin-top: 0.35em;
  padding-left: 0.5em;
  font-size: 0.95rem;
}

.btn {
  position: relative;
  top: 0.25em;
}

.answer {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 3.125em;
  font-weight: bold;
}

.loading-data {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 1em;
  font-size: 3rem;
}

.question {
  font-weight: bold;
}

.number {
  margin-right: 2px;
}
</style>
