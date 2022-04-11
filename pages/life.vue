<template>
  <div class="splash-screen">
    <div class="spinner-wrapper">
      <div class="spinner"></div>
    </div>
  </div>
</template>
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
<script>
// import ExampleAnalyticsService from "./example-analytics-service";
export default {
  data() {
    return {
      isLoading: true,
      property: "Example property.",
      counter: 0,
      exampleLeakyProperty:
        "This represents a property that will leak memory if not cleaned up.",
    };
  },
  computed: {
    propertyComputed() {
      return this.property;
    },
  },
  beforeCreate() {
    this.showHideSpinner = true;
  },
  mounted() {
    this.showHideSpinner = false;
  },
  beforeCreate() {
    console.log("At this point, events and lifecycle have been initialized.");
  },
  created() {
    console.log(
      "At this point, this.property is now reactive and propertyComputed will update."
    );
    this.property = "Example property updated.";
    setInterval(() => {
      this.counter++;
    }, 1000);
  },
  beforeMount() {
    console.log(`At this point, vm.$el has not been created yet.`);
  },
  mounted() {
    console.log(
      `At this point, vm.$el has been created and el has been replaced.`
    );
    console.log(this.$el.textContent); // Example component.
  },
  beforeUpdate() {
    console.log(
      `At this point, Virtual DOM has not re-rendered or patched yet.`
    );
    // Logs the counter value every second, before the DOM updates.
    console.log(this.counter);
  },
  updated() {
    console.log(`At this point, Virtual DOM has re-rendered and patched.`);
    // Fired every second, should always be true
    console.log(+this.$refs["example-element"].textContent === this.counter);
  },
  //   beforeDestroy() {
  //     console.log(
  //       `At this point, watchers, child components, and event listeners have not been teared down yet.`
  //     );
  //     // Perform the teardown procedure for exampleLeakyProperty.
  //     // (In this case, effectively nothing)
  //     this.exampleLeakyProperty = null;
  //     delete this.exampleLeakyProperty;
  //   },
  //   destroyed() {
  //     console.log(
  //       `At this point, watchers, child components, and event listeners have been torn down.`
  //     );
  //     console.log(this);
  //     ExampleAnalyticsService.informService("Component destroyed.");
  //   },
};
</script>
