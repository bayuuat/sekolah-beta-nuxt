<template>
  <div class="splash-screen">
    <div class="spinner"></div>
  </div>
</template>
<style scoped>
.splash-screen {
  background: #f2f0ee;
  width: 100vw;
  height: 100vh;
  position: fixed;
  display: flex;
  z-index: 100;
  align-items: center;
  justify-content: center;
}

.spinner {
  width: 50px;
  height: 50px;
  border: 5px solid;
  color: coral;
  border-radius: 50%;
  border-top-color: transparent;
  opacity: 0%;
  animation: loading 1.2s linear infinite;
}

@keyframes loading {
  25% {
    color: blueviolet;
  }
  50% {
    color: rgb(192, 226, 43);
  }
  75% {
    opacity: 100%;
    color: rgb(226, 43, 43);
  }
  to {
    transform: rotate(360deg);
  }
}
</style>
