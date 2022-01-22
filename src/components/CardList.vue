<template>
  <div class="card-list">
    <SingelCard v-if="!savedCardsArray" :card="card" class="single-card" />
    <SingelCard
      @wasClicked="changeActive(index)"
      :card="card"
      v-else
      v-for="(card, index) in savedCardsArray"
      :key="card.index"
      :class="{ active: index === 0 }"
    />
  </div>
</template>

<script>
import SingelCard from "./SingelCard.vue";
export default {
  mounted() {
    this.savedCardsArray = JSON.parse(localStorage.getItem("savedCards"));
  },
  data() {
    return {
      savedCardsArray: [],
      card: {
        cardNumber: "",
        cardholderName: "",
        month: "",
        year: "",
        vendor: {},
      },
    };
  },
  components: { SingelCard },
  methods: {
    changeActive(index) {
      if (index > 0) {
        let newActive = this.savedCardsArray[index];
        this.savedCardsArray.splice(index, 1);
        this.savedCardsArray.unshift(newActive);
      }
    },
  },
};
</script>

<style scoped>
.single-card:not(:first-of-type):hover {
  transform: translateY(-20%);
}
</style>
