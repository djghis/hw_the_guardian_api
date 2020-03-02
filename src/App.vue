<template>
  <div id="app">
    <img id="logo" src="./assets/the-guardian-logo1.jpg" >
    <h1>Please Select an article</h1>
    <input type="text" name="search" :subjectSearch="subjectSearch" value="" placeholder="Subject to search" v-model="subjectSearch" >
    <!-- <button type="button" name="button" value="Search" @click="handleClick()"></button> -->
    <input type="submit" name="Search" value="Search" @click="handleClick(subjectSearch)">
    <!-- <search :subjectSearch="subjectSearch" /> -->
    <article-select :articles="articles"/>
    <h3>Article preview (if it ever works)</h3>
    <h5>if there is no preview click in the link below</h5>
    <article-view :article="selectedArticle"/>
    <!-- <link-prevue url="article.webUrl" :article="selectedArticle"></link-prevue> -->
  </div>
</template>

<script>
import ArticleSelect from './components/ArticleSelect.vue'
import LinkPrevue from 'link-prevue'
import {eventBus} from './main.js'
import ArticleView from './components/ArticleView.vue'
import Search from './components/Search'
export default {
  name: 'App',
  data(){
    return {
      articles: [],
      selectedArticle: {},
      subjectSearch: null
    }
  },
  components: {
    'article-select': ArticleSelect,
    'article-view': ArticleView,
    'link-prevue': LinkPrevue
  },
  mounted(){
    fetch("https://content.guardianapis.com/search?q=latest&format=json&api-key=05340d8a-f0bf-454d-8140-4cc72caafd0d")
    .then(response => response.json())
    .then(articleData => this.articles = articleData.response.results)
// console.log(articleData.response.results)
    eventBus.$on("article-selected", (article) => {
      this.selectedArticle= article;
    })
},
methods: {
  handleClick: function(subjectSearch){
    const url = `https://content.guardianapis.com/search?q=${subjectSearch}&format=json&api-key=05340d8a-f0bf-454d-8140-4cc72caafd0d`;
    fetch(url)
    .then(response => response.json())
    .then(articleData => this.articles = articleData.response.results)
// console.log(articleData.response.results)
    eventBus.$on("article-selected", (article) => {
      this.selectedArticle= article;
    })
  }
}
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
  background-image: linear-gradient(lightgrey, blue);
}

#logo {
  height: 10rem;
  background-color: lightgrey;
}
</style>
