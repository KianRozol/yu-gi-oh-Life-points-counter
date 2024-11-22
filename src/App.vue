<template>
  <div id="app">
    <div class="counter">
      <h1>WELCOME TO YU-GI-OH LIFE POINTS COUNTER</h1>
      <h2>LIFE POINTS &nbsp; {{ count }}</h2>

      <button
        @mousedown="startIncrementAction('increment')"
        @mouseup="stopAction"
        @mouseleave="stopAction"
      >
        Add Power
      </button>

      <button
        @mousedown="startIncrementAction('decrement')"
        @mouseup="stopAction"
        @mouseleave="stopAction"
      >
        Reduce Power
      </button>

      <button @click="reset">Reset</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      count: 8000,
      interval: null,
      isSmallScreen: false,
    };
  },

  methods: {
    increment() {
      this.count += 1;
    },
    decrement() {
      this.count -= 1;
    },

    startIncrementAction(action) {
      if (!this.interval) {
        this.interval = setInterval(() => {
          if (action === "increment") {
            this.increment();
          } else if (action === "decrement") {
            this.decrement();
          }
        }, 50);
      }
    },

    stopAction() {
      if (this.interval) {
        clearInterval(this.interval);
        this.interval = null;
      }
    },

    reset() {
      this.count = 8000;
    },
    checkScreenSize() {
      this.isSmallScreen = window.innerWidth <= 600;
    },
  },

  mounted() {
    this.checkScreenSize();
    window.addEventListener("resize", this.checkScreenSize);
  },
  beforeDestroy() {
    window.removeEventListener("resize", this.checkScreenSize);
  },
};
</script>

<style scoped>
.counter {
  text-align: center;
  margin-top: 50px;
}
h1 {
  color: rgb(255, 5, 5);
}
h2 {
  color: rgb(253, 0, 0);
}
button {
  margin: 10px;
  padding: 10px 20px;
  font-size: 18px;
  cursor: pointer;
}

button:hover {
  background-color: brown;
}

/* Add background image */
#app {
  background-image: url("@/assets/bg.jpg");
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;

  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
  height: 100vh;
  width: 100vw;
  display: flex;
  justify-content: center;
  align-items: center;
}

@media (max-width: 600px) {
  h1 {
    font-size: 18px;
  }

  h2 {
    font-size: 16px;
  }

  button {
    padding: 8px 16px;
    font-size: 14px;
  }
}

html,
body {
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
}
</style>
