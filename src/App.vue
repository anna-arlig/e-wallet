<template>
  <div class="app">
    <div v-if="confirmView" class="confirm">
      <div class="inner-confirm">
        <h2>Are you sure that you want to delete this card?</h2>
        <button class="confirm-btn" @click="removeCard">
          Yes, delete this card
        </button>
        <button class="confirm-btn" @click="confirmView = false">
          No, take me back
        </button>
      </div>
    </div>
    <Home
      v-if="currentview == 'home'"
      @viewChange="changeView"
      :savedCardsArray="savedCardsArray"
      @showConfirm="showConfirm"
    />
    <AddCard v-else @viewChange="changeView" @saveCard="saveCard" />
  </div>
</template>

<script>
import Home from "./views/Home.vue";
import AddCard from "./views/AddCard.vue";

export default {
  mounted() {
    this.savedCardsArray = JSON.parse(localStorage.getItem("savedCards"));
  },
  methods: {
    removeCard(index) {
      this.savedCardsArray.splice(index, 1);
      localStorage.setItem("savedCards", JSON.stringify(this.savedCardsArray));
      this.confirmView = false;
    },

    showConfirm() {
      if (this.confirmView) {
        this.confirmView = false;
      } else {
        this.confirmView = true;
      }
    },
    saveCard(card) {
      this.savedCardsArray.push(card);
      localStorage.setItem("savedCards", JSON.stringify(this.savedCardsArray));
    },
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
      confirmView: false,
      savedCardsArray: [],
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

h2 {
  font-size: 15px;
}

.confirm {
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  z-index: 15;
  background-color: rgba(0, 0, 0, 0.4);
  height: 100vh;
  width: 100vh;
  margin: 0;
}

.inner-confirm {
  position: absolute;
  display: flex;
  flex-direction: column;
  background-color: white;
  color: black;
  text-align: center;
  padding: 30px;
}

.confirm-btn {
  font-size: 15px;
  margin: 5px;
}

.confirm-btn:first-of-type {
  background-color: rgb(0, 0, 0);
  color: white;
}

button {
  background-color: white;
  border-radius: 5px;
  border: 2px solid black;
  font-size: 18px;
  font-weight: 600;
  min-height: 50px;
  padding-left: 100px;
  padding-right: 100px;
  margin: auto;
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
