<template>
  <div>
    <form class="header" @submit.prevent="handleSubmit">
      <div class="form-group">
        <label for="category">Category</label>
        <select id="category" v-if="categories" v-model="selected">
          <option :key="item.id" :value="item.id" v-for="item in categories">
            {{ item.name }}
          </option>
        </select>
      </div>
      <div class="form-group">
        <label for="amount">Number of Questions</label>
        <input
          type="number"
          id="amount"
          min="1"
          max="50"
          step="1"
          v-model="input"
        />
      </div>
      <div class="btn">
        <button>Generate</button>
      </div>
    </form>
    <h3 v-if="loading" class="loading-data">Loading questions...</h3>
  </div>
</template>

<script>
export default {
  name: "Header",
  props: {
    loading: Boolean,
    categories: Array,
  },
  data() {
    return {
      selected: "",
      input: "",
    };
  },

  methods: {
    async handleSubmit() {
      this.$emit("setLoadingToTrue");
      try {
        const response = await fetch(
          "https://opentdb.com/api.php?amount=" +
            this.input +
            "&category=" +
            this.selected
        );
        const json = await response.json();
        this.$emit("send-cards", json);
      } catch (err) {
        console.log(err);
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
button {
  padding: 0.3125em;
  background-color: rgb(65, 65, 131);
  color: white;
  cursor: pointer;
  margin-bottom: 0;
}

select {
  width: 271px;
}

.loading-data {
  text-align: center;
}

.header {
  display: flex;
  align-items: center;
  justify-content: center;
}

.form-group {
  margin: 0.5em;
  display: flex;
  flex-direction: column;
}

.btn {
  position: relative;
  top: 0.25em;
}

button {
  padding: 0.3125em;
  background-color: rgb(65, 65, 131);
  color: white;
  cursor: pointer;
  margin-bottom: 0;
}
</style>
