<template lang="html">
  <div class="">
    <h2>{{article.webTitle}}</h2>
    <a :href="article.webUrl" target="_blank">Click here to open the article in a new tab</a>
    <div>
    <object type="text/html" :data="this.article.webUrl" width="800px" height="600px" style="overflow:auto;border:5px ridge blue">
    </object>
 </div>
  </div>
</template>

<script>
export default {
  name: "article-view",
  props: ["article",
          "subjectSearch"]
}
</script>

<style lang="css" scoped>
</style>
