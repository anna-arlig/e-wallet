<template>
  <div>
    <SingelCard :card="card" :vendors="vendors" />
    <form class="user-form" @submit.prevent="'submit', card">
      <label for="card-number">CARD NUMBER</label>
      <input type="text" name="cardholder-name" v-model="card.cardNumber" />
      <label for="cardholder-name">CARDHOLDER NAME</label>
      <input type="text" name="cardholder-name" v-model="card.cardholderName" />
      <label for="month">MONTH</label>
      <select id="months" name="months" v-model="card.month">
        <option v-for="month in months" :key="month" value:value="month">
          {{ month }}
        </option>
      </select>
      <label for="year">YEAR</label>
      <select id="year" name="year" v-model="card.year">
        <option v-for="year in years" :key="year" name="year">
          {{ year }}
        </option>
      </select>
      <label for="vendor">VENDOR</label>
      <select id="vendor" name="vendor" v-model="card.vendor">
        <option
          v-for="vendor in vendors"
          :key="vendor.name"
          name="vendor"
          :value="vendor"
        >
          {{ vendor.name }}
        </option>
      </select>
      <input
        class="submit-btn"
        @click="$emit('viewChange')"
        @submit="submit"
        type="submit"
        value="ADD CARD"
      />
    </form>
  </div>
</template>

<script>
import SingelCard from "./SingelCard.vue";
export default {
  components: { SingelCard },
  data() {
    return {
      card: {
        cardNumber: "",
        cardholderName: "",
        month: "",
        year: "",
        vendor: "",
      },

      vendors: [
        {
          name: "Bitcoin Inc",
          backgroundColor: "#FFAE34",
          fontColor: "white",
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

      months: [
        "01",
        "02",
        "03",
        "04",
        "05",
        "06",
        "07",
        "08",
        "09",
        "10",
        "11",
        "12",
      ],
      years: ["2022", "2023", "2024", "2025", "2026"],
    };
  },
  methods: {
    submit() {
      this.$emit("send", { ...this.card });
    },
  },
};
</script>

<style scoped>
.user-form {
  display: flex;
  flex-direction: column;
}
.submit-btn {
  background-color: black;
  color: white;
  border-radius: 5px;
  border: 2px solid black;
  font-size: 18px;
  font-weight: 600;
  min-height: 50px;
  padding-left: 130px;
  padding-right: 130px;
  margin: auto;
  margin-top: 40px;
}
</style>
