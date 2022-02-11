<template>
  <div v-if="showCards" class="card-grid">
    <div :key="flashcard.id" v-for="flashcard in flashCards">
      <FlashCard :flashcard="flashcard" />
    </div>
  </div>
</template>

<script>
import FlashCard from "../components/FlashCard.vue";
export default {
  name: "FlashCardList",
  components: { FlashCard },
  props: {
    flashCards: Array,
    loading: Boolean,
  },

  computed: {
    showCards() {
      return this.flashCards !== null && this.loading === false;
    },
  },
};
</script>

<style lang="scss" scoped>
.card-grid {
  display: grid;
  align-items: center;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 2.3em;
  margin-top: 3.25em;
}
</style>
