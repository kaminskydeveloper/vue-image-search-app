<template>
  <div id="app">
    <h1>{{title}}</h1>
    <form @submit.prevent="formSubmitted()">
      <label for="searchTerm">Search Term</label>
      <input
        v-model="searchTerm"
        type="text"
        id="searchTerm"
        name="searchTerm"
        class="u-full-width"
      />
      <button type="submit">Serach</button>
    </form>
    <img v-if="loading" src="https://i.imgur.com/5sHokPz.gif" alt="loading..." />
    <section class="images">
      <img v-for="image in images" :key="image.id" :src="image.urls.full" alt="">
    </section>
  </div>
</template>

<script>
import API from "./api";
export default {
  name: "app",
  data() {
    return {
      title: "Vue Image Search",
      searchTerm: "",
      images: [],
      loading: false
    };
  },
  methods: {
    formSubmitted() {
      this.images = [];
      this.loading = true;
      API.search(this.searchTerm).then(images => {
        this.images = images;
        this.loading = false;
      });
      this.searchTerm = "";
    }
  }
};
</script>

<style>
body {
  width: 80%;
  margin: 2em auto 0 auto;
}

img {
  width: 100%;
}

.images {
  column-count: 3;
}
</style>
