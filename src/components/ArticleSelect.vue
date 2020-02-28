<template lang="">

  <select>
    <option v-for="article in articles">{{article.webTitle}}</option>

</select>
</template>

<script>
export default {
  name: "article-select",
  props: ["articles"]

}
</script>

<style lang="css" scoped>
</style>
