<template>
  <div class="card-list">
    <SingelCard v-if="!savedCardsArray" :card="card" class="single-card" />
    <SingelCard
      :allowDelete="index === 0"
      @wasClicked="changeActive(index)"
      @showDelete="showDelete(index)"
      @hideDelete="hideDelete(index)"
      @showConfirm="showConfirm"
      :card="card"
      v-else
      v-for="(card, index) in savedCardsArray"
      :key="card.index"
      :class="{ active: index === 0 }"
      :style="{ zIndex: index }"
    />
    <!-- Detta borde gå att lösa bättre -->
    <button
      class="empty-btn"
      v-if="!savedCardsArray"
      @click="$emit('viewChange')"
    >
      ADD A NEW CARD
    </button>
    <button class="full-btn" v-else @click="$emit('viewChange')">
      ADD A NEW CARD
    </button>
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
      confirmView: false,
      allowDelete: false,
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
    hideDelete(index) {
      if (index === 0) {
        this.deleteBtn = false;
      }
    },
    showDelete(index) {
      if (index === 0) {
        this.deleteBtn = true;
      }
    },

    // Funkar inte, flytta till AddCard?

    showConfirm() {
      if (this.confirmView === true) {
        this.confirmView = false;
      } else {
        this.confirmView = true;
      }
    },

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

.single-card:not(:first-of-type) {
  position: relative;
  margin-bottom: -180px;
}

.full-btn {
  margin-top: 210px;
}
.empty-btn {
  margin-top: 80px;
}
</style>
