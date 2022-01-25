<template>
  <div>
    <SingelCard :card="card" :vendors="vendors" />
    <form class="user-form" @submit.prevent="submit">
        <p v-if="errors.length">
    <b>Please correct the following error(s):</b>
    <ul>
      <li v-for="error in errors" :key="error">{{ error }}</li>
    </ul></p>
      <label for="card-number">CARD NUMBER</label>
      <input type="number" name="cardnumber" v-model="card.cardNumber" />
      <label for="cardholder-name">CARDHOLDER NAME</label>
      <input type="text" name="cardholder-name" v-model="card.cardholderName" />

      <div class="date">
        <div class="valid">
          <label for="month">MONTH</label>
          <select name="months" v-model="card.month" class="date-select">
            <option v-for="month in months" :key="month" value:value="month">
              {{ month }}
            </option>
          </select>
        </div>

        <div class="valid">
          <label for="year">YEAR</label>
          <select name="year" v-model="card.year" class="date-select">
            <option v-for="year in years" :key="year" name="year">
              {{ year }}
            </option>
          </select>
        </div>
      </div>

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
        @click="validate"
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
      errors: [],
      savedCardsArray: [],
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
    validate(e) {

        this.errors = [];

    if (localStorage.getItem("savedCards") != undefined){
this.savedCardsArray = JSON.parse(localStorage.getItem("savedCards"));}
        for (let element of this.savedCardsArray){
            if (element.cardNumber == this.card.cardNumber){
                this.errors.push('Cardnumber needs to be unique.');
            }
        }

    // if (!/[^a-zA-Z]/.test(this.cardholderName)){
    //     this.errors.push('Only letters in Cardholder name')
    // }

      if (this.card.cardNumber === "") {
        this.errors.push('Cardnumber required.');
      }
      if (this.card.cardholderName === "") {
        this.errors.push('Cardholder name required.');
      }
         if (this.card.month === "") {
        this.errors.push('Month required.');
      }
         if (this.card.year === "") {
        this.errors.push('Year required.');
      }
         if (Object.keys(this.card.vendor).length === 0 && this.card.vendor.constructor === Object) {
        this.errors.push('Vendor required.');
      }

      e.preventDefault()

     if (!this.errors.length) {
        this.$emit("viewChange");
      }
    },
  },
  beforeDestroy() {
    if (localStorage.getItem("savedCards") != undefined) {
      this.savedCardsArray = JSON.parse(localStorage.getItem("savedCards"));
    }
    this.savedCardsArray.push(this.card);
    localStorage.setItem("savedCards", JSON.stringify(this.savedCardsArray));
  },
};
</script>

<style scoped>
.date-select {
  min-width: 160px;
}

input {
  min-height: 25px;
}

select {
  min-height: 30px;
}

.date {
  display: flex;
  justify-content: space-between;
}

label {
  margin: 5px;
  margin-top: 10px;
}

.valid {
  display: flex;
  flex-direction: column;
}

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
