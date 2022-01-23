<template>
  <div class="app">
    <Home v-if="currentview == 'home'" @viewChange="changeView" />
    <AddCard v-else @viewChange="changeView" />
  </div>
</template>

<script>
import Home from "./views/Home.vue";
import AddCard from "./views/AddCard.vue";
export default {
  methods: {
    changeView() {
      if (this.currentview == "home") {
        this.currentview = "AddCard";
      } else {
        this.currentview = "home";
      }
    },
  },
  components: { Home, AddCard },
  data() {
    return {
      currentview: "home",
    };
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=PT+Mono&family=Source+Sans+Pro:wght@400;600&display=swap");
* {
  font-family: "PT Mono", monospace;
  font-size: 10px;
}

h1 {
  font-family: "Source Sans Pro", sans-serif;
  text-transform: uppercase;
  text-align: center;
  max-width: 200px;
  margin: auto;
  line-height: 2.5rem;
  font-size: 30px;
  margin-bottom: 30px;
}

p {
  text-transform: uppercase;
  font-family: "Source Sans Pro", sans-serif;
  text-align: center;
}

.app {
  display: flex;
  justify-content: center;
  margin: auto;
}
</style>
