<template>
  <div class="home-view">
    <h1>E-Wallet</h1>
    <p :style="{ color: 'darkgrey' }">Active card</p>

    <CardList
      @viewChange="$emit('viewChange')"
      :savedCardsArray="savedCardsArray"
      @showConfirm="$emit('showConfirm', $event)"
    />
  </div>
</template>

<script>
import { CardList } from "../components";

export default {
  props: ["savedCardsArray"],
  methods: {},

  data() {
    return {};
  },
  components: { CardList },
};
</script>

<style scoped>
.home-view {
  display: flex;
  flex-direction: column;
  justify-content: center;
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
  margin-top: 210px;
}
</style>
