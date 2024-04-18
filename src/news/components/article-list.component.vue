<script>
  import ArticleCard from "./article-card.component.vue";

  export default{
    name: "article-list",
    components: {ArticleCard},
    props: {
      articles: Array
    }
  }
</script>
<!-- IN THIS STAGE, WE USE A FOR PROPERTY TO LIST ALL THE CARDS -->
<template>
  <div v-for="article in articles">
    <article-card :article="article" /> <!-- IN HERE WE CALL THE PROPERTY "article" FROM THE COMPONENT ARTICLE -->
  </div>
</template>
