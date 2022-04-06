<template>
  <div id="app">
    <Header />
    <Nuxt />
    <Footer />
  </div>
</template>

<script>
// Memanggil component sesuai lokasi masing - masing file
import Header from "@/components/header.vue";
import Footer from "@/components/footer.vue";
export default {
  // Dideklarasikan agar dapat diakses oleh template
  components: {
    Header,
    Footer,
  },
};
</script>
<style></style>
