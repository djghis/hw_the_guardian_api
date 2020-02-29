<template lang="html">
  <div class="">
    <h2>{{article.webTitle}}</h2>
    <a :href="article.webUrl">{{article.webUrl}}</a>
  </div>
</template>

<script>
export default {
  name: "article-view",
  props: ["article"]
}
</script>

<style lang="css" scoped>
</style>
