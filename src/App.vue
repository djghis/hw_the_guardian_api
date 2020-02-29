<template>
  <div id="app">
    <h1>Please Select an article</h1>
    <article-select :articles="articles"/>
    <article-view :article="selectedArticle"/>

  </div>
</template>

<script>
import ArticleSelect from './components/ArticleSelect.vue'
import {eventBus} from './main.js'
import ArticleView from './components/ArticleView.vue'
export default {
  name: 'App',
  data(){
    return {
      articles: [],
      selectedArticle: {}
    }
  },
  components: {
    'article-select': ArticleSelect,
    'article-view': ArticleView
  },
  mounted(){
    fetch("https://content.guardianapis.com/search?q=cars&format=json&api-key=05340d8a-f0bf-454d-8140-4cc72caafd0d")
    .then(response => response.json())
    .then(articleData => this.articles = articleData.response.results)
// console.log(articleData.response.results)
    eventBus.$on("article-selected", (article) => {
      this.selectedArticle= article;
    })
},
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
