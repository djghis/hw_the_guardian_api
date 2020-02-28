<template>
  <div id="app">
    <h1>Please Select an article</h1>
    <article-select :articles="articles"/>
  </div>
</template>

<script>
import ArticleSelect from './components/ArticleSelect.vue'

export default {
  name: 'App',
  data(){
    return {
      articles: []
    }
  },
  components: {
    'article-select': ArticleSelect
  },
  mounted(){
    fetch("https://content.guardianapis.com/search?q=cars&format=json&api-key=test")
    .then(response => response.json())
    .then(articleData => this.articles = articleData.response.results)
// console.log(articleData.response.results)
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
