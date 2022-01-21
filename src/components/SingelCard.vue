<template>
  <div class="single-card">
    <div
      class="card"
      v-bind:style="{ backgroundColor: card.vendor.backgroundColor }"
    >
      <img :src="wifiImg" alt="Wifi logo" />
      <img :src="chipImg" alt="Chip logo" />
      <img :src="card.vendor.logo" alt="Vendor logo" />

      <p>{{ card.cardNumber }}</p>
      <p>CARDHOLDER NAME</p>
      <p>{{ card.cardholderName }}</p>
      <p>{{ card.month }}</p>
      <p>{{ card.year }}</p>
      <p>{{ card.vendor.name }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["card", "vendors"],
  data() {
    return {
      wifiImg: require("../assets/wifi.svg"),
      chipImg: require("../assets/chip.svg"),
      whiteWifiImg: require("../assets/wifi_white.svg"),
      vendorLogo: this.card.vendor.logo,
    };
  },
};
</script>

<style scoped>
.card {
  background-color: #d0d0d0;
  border-radius: 5px;
  min-width: 350px;
  min-height: 200px;
  box-shadow: 0px 0px 5px 5px rgba(0, 0, 0, 0.19);
  margin-bottom: 40px;
}
p {
  color: black;
}
</style>
