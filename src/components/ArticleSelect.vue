<template lang="">

  <select @change="handlechange" v-model="selectedArticle">
    <option v-for="article in articles" :value="article">{{article.webTitle}}</option>

</select>
</template>

<script>
import {eventBus} from "../main.js"
export default {
  name: "article-select",
  props: ["articles"],
  data(){
    return {
      selectedArticle: {}
    }
  },
  methods: {
    handlechange: function(){
      eventBus.$emit("article-selected", this.selectedArticle)
    }
  }

}
</script>

<style lang="css" scoped>
</style>
