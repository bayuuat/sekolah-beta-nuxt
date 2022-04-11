<template>
  <div id="app">
    <Loading v-if="isLoading" />
    <div>
      <Header />
      <Nuxt />
      <Footer />
    </div>
  </div>
</template>

<script>
// Memanggil component sesuai lokasi masing - masing file
import Header from "@/components/header.vue";
import Footer from "@/components/footer.vue";
import Loading from "@/components/loading.vue";
export default {
  // Dideklarasikan agar dapat diakses oleh template
  components: {
    Header,
    Footer,
    Loading,
  },
  data() {
    return {
      isLoading: true,
    };
  },
  beforeCreate() {
    this.isLoading = true;
  },
  mounted() {
    setTimeout(() => {
      this.isLoading = false;
    }, 3000);
  },
};
</script>
<style scoped>
.splash-screen {
  background: #f2f0ee;
  width: 100vw;
  height: 100vh;
  position: fixed;
  z-index: 50;
}

.spinner-wrapper {
  position: absolute;
  left: 50%;
  top: 50%;

  transform: translate(-50%, -50%);
}
.spinner {
  width: 80px;
  height: 80px;
  margin: 100px auto;
  background-color: #e45447;

  border-radius: 100%;
  -webkit-animation: sk-scaleout 1s infinite ease-in-out;
  animation: sk-scaleout 1s infinite ease-in-out;
}

@-webkit-keyframes sk-scaleout {
  0% {
    -webkit-transform: scale(0);
  }
  100% {
    -webkit-transform: scale(1);
    opacity: 0;
  }
}

@keyframes sk-scaleout {
  0% {
    -webkit-transform: scale(0);
    transform: scale(0);
  }
  100% {
    -webkit-transform: scale(1);
    transform: scale(1);
    opacity: 0;
  }
}
</style>
