<template>
  <div>
    <div class="title">
      <h1>mi a fasz tortenik itt</h1>
    </div>
    <div class="container">
      <div  v-for="article in filteredList" v-bind:key="article" class="max-w-sm rounded overflow-hidden shadow-lg p-1">
        <img
          class="w-full"
          :src="'http://localhost:1337' + article.assets[0].url" alt="" width="300" height="300" 
        />
        <div class="px-6 py-4">
          <div class="font-bold text-xl mb-2">{{ article.title }}</div>
          <p
            class="text-gray-700 text-base"
          >{{ article.content }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import articlesQuery from "~/apollo/queries/article/articles";

export default {
  data() {
    return {
      articles: [],
      query: ""
    };
  },
  apollo: {
    articles: {
      prefetch: true,
      query: articlesQuery
    }
  },
  computed: {
    filteredList() {
      return this.articles.filter(article => {
        return article.title.toLowerCase().includes(this.query.toLowerCase());
      });
    }
  }
};
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 90vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  padding: top 1rem;
  text-align: center;
  font-size: 50px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
