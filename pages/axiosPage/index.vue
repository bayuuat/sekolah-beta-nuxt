<template>
  <div id="app">
    <Header />
    <main class="container">
      <Hero />
      <div class="row mb-2">
        <!-- <Article /> -->
        <Article
          v-for="(article, index) in articles"
          :key="index"
          :article="article"
        />
      </div>
    </main>
  </div>
</template>

<script>
import Header from "@/components/TheHeader.vue";
import Hero from "@/components/TheHero.vue";
import Article from "@/components/CardArticle.vue";

export default {
  components: {
    Header,
    Hero,
    Article,
  },
  data() {
    return {
      articles: [],
    };
  },
  async fetch() {
    await this.$axios
      .get("v1/cnn-news")
      .then((res) => (this.articles = res.data.data));
  },
  mounted() {
    // console.log("Artikel: ", this.articles);
  },
};
</script>

<style></style>
