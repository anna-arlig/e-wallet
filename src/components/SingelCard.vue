<template>
  <div
    class="single-card"
    @click="$emit('wasClicked')"
    @mouseenter="allowDelete ? (deleteBtn = true) : null"
    @mouseleave="allowDelete ? (deleteBtn = false) : null"
  >
    <div class="card" v-bind:style="cardStyle">
      <span class="upperpart">
        <div class="logos">
          <img :src="wifi" alt="Wifi logo" id="wifiImg" />
          <img src="../assets/chip.svg" alt="Chip logo" id="chipImg" />
        </div>
        <img :src="logo" alt="Vendor logo" />
      </span>

      <button
        class="delete-btn"
        v-if="deleteBtn"
        @click.stop="$emit('showConfirm')"
      >
        Delete this card
      </button>

      <span class="middlepart"
        ><p id="cardnum">{{ cardNum }}</p></span
      >
      <span class="bottompart">
        <div class="name">
          <p class="cardheader">CARDHOLDER NAME</p>
          <p class="cardinfo">{{ holderName }}</p>
        </div>
        <div class="valid">
          <p class="cardheader">VALID THRU</p>
          <p class="cardinfo">{{ `${validMonth}/${validYear}` }}</p>
        </div>
      </span>
    </div>
  </div>
</template>

<script>
export default {
  computed: {
    wifi() {
      return this.card.vendor.name == "Ninja Bank"
        ? this.whiteWifiImg
        : this.wifiImg;
    },

    cardStyle() {
      return {
        backgroundColor: this.card.vendor.backgroundColor,
        color: this.card.vendor.fontColor,
      };
    },

    logo() {
      return this.card.vendor.logo ? this.card.vendor.logo : this.vendorLogo;
    },

    cardNum() {
      let span = "";
      if (this.card.cardNumber) {
        let sub1 = this.card.cardNumber.substring(0, 4);
        let sub2 = this.card.cardNumber.substring(4, 8);
        let sub3 = this.card.cardNumber.substring(8, 12);
        let sub4 = this.card.cardNumber.substring(12, 16);
        span = `${sub1} ${sub2} ${sub3} ${sub4}`;
      } else {
        span = `XXXX XXXX XXXX XXXX`;
      }
      return span;
    },
    holderName() {
      return this.card.cardholderName
        ? this.card.cardholderName
        : `Firstname Lastname`;
    },
    validMonth() {
      return this.card.month ? this.card.month : `XX`;
    },
    validYear() {
      return this.card.year ? this.card.year : `XX`;
    },
  },
  props: ["card", "vendors", "allowDelete"],
  data() {
    return {
      deleteBtn: false,
      wifiImg: require("../assets/wifi.svg"),
      chipImg: require("../assets/chip.svg"),
      whiteWifiImg: require("../assets/wifi_white.svg"),
      vendorLogo: require("../assets/bitcoin.svg"),
    };
  },
  methods: {},
};
</script>

<style scoped>
.delete-btn {
  min-width: 200px;
  padding: 0px;
  margin-left: 80px;
  position: absolute;
}
.name {
  margin-left: 15px;
}
.valid {
  margin-right: 15px;
}
.cardheader {
  font-size: 10px;
  font-family: "PT Mono", monospace;
  text-align: left;
}

.cardinfo {
  font-size: 15px;
  font-family: "PT Mono", monospace;
  margin-top: 5px;
}

#cardnum {
  font-size: 23px;
  letter-spacing: 0.3rem;
  margin-top: 10px;
  font-family: "PT Mono", monospace;
}

#wifiImg {
  max-width: 40px;
}

#chipImg {
  max-width: 40px;
}

.logos {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 20px;
  margin-left: 20px;
}
.upperpart {
  display: flex;
  justify-content: space-between;
}
.bottompart {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.card {
  background-color: #d0d0d0;
  border-radius: 5px;
  min-width: 350px;
  min-height: 200px;
  box-shadow: 0px 0px 10px 1px rgba(0, 0, 0, 0.81);
  margin-bottom: 30px;
}
</style>
