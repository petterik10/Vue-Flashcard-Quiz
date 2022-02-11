<template>
  <div class="container">
    <Header />
    <Form
      :categories="categories"
      @send-cards="receivedCards"
      @setLoadingToTrue="loading = true"
      :loading="loading"
    />
    <FlashCardList :flashCards="cards" :loading="loading" />
  </div>
</template>

<script>
import Form from "./components/Form.vue";
import Header from "./components/Header.vue";
import FlashCardList from "./components/FlashCardList.vue";
export default {
  name: "App",
  components: {
    Header,
    Form,
    FlashCardList,
  },
  data() {
    return {
      categories: [],
      cards: [],
      loading: false,
    };
  },

  methods: {
    decodeHtml(html) {
      let txt = document.createElement("textarea");
      txt.innerHTML = html;
      return txt.value;
    },
    receivedCards(newCards) {
      this.loading = false;
      const receivedCards = newCards.results.map((elem, i) => {
        const correctAnswer = this.decodeHtml(elem.correct_answer);
        const options = [
          ...elem.incorrect_answers.map((elem) => {
            return this.decodeHtml(elem);
          }),
          correctAnswer,
        ];
        return {
          id: `${i} - ${Date.now()}`,
          question: this.decodeHtml(elem.question),
          answer: this.decodeHtml(elem.correct_answer),
          options: options.sort(() => Math.random() - 0.5),
        };
      });
      this.cards = receivedCards;
    },
    async fetchCategories() {
      const res = await fetch("https://opentdb.com/api_category.php");
      const data = await res.json();
      return data.trivia_categories;
    },
  },
  async created() {
    this.categories = await this.fetchCategories();
  },
};
</script>

<style lang="scss">
* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}

body {
  background-image: url("https://www.transparenttextures.com/patterns/45-degree-fabric-light.png");
}

.container {
  max-width: 900px;
  margin: 0 auto;
}
</style>
