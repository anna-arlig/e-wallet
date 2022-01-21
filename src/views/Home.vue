<template>
  <div class="home-view">
    <h1>E-Wallet</h1>
    <p>Active card</p>
    <SingelCard />
    <CardList />
    <button @click="$emit('viewChange')">ADD A NEW CARD</button>
  </div>
</template>

<script>
import { CardList, SingelCard } from "../components";

export default {
  methods: {},
  components: { CardList, SingelCard },
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
  margin-top: 40px;
}
</style>
