<template>
  <div class="card-list">
    <SingelCard :card="card" :vendors="vendors" @submit="saveCard" />
  </div>
</template>

<script>
import SingelCard from "./SingelCard.vue";
export default {
  data() {
    return {
      savedCards: [],
      wifiImg: require("../assets/wifi.svg"),
      chipImg: require("../assets/chip.svg"),
      whiteWifiImg: require("../assets/wifi_white.svg"),
      vendorLogo: require("../assets/bitcoin.svg"),
      card: {
        cardNumber: "",
        cardholderName: "",
        month: "",
        year: "",
        vendor: {},
      },
      vendors: [
        {
          name: "Bitcoin Inc",
          backgroundColor: "#FFAE34",
          fontColor: "black",
          logo: require("../assets/bitcoin.svg"),
        },
        {
          name: "Ninja Bank",
          backgroundColor: "#222222",
          fontColor: "white",
          logo: require("../assets/ninja.svg"),
        },
        {
          name: "Block Chain Inc",
          backgroundColor: "#8B58F9",
          fontColor: "white",
          logo: require("../assets/blockchain.svg"),
        },
        {
          name: "Evil Corp",
          backgroundColor: "#F33355",
          fontColor: "white",
          logo: require("../assets/evil.svg"),
        },
      ],
    };
  },
  components: { SingelCard },
  methods: {
    saveCard() {
      this.savedCards.push("savedCards");
    },
  },
};
</script>

<style></style>
