<template>
  <div class="card-list">
    <button class="delete-btn" v-if="deleteBtn" @click="showConfirm">
      Delete this card
    </button>
    <SingelCard v-if="!savedCardsArray" :card="card" class="single-card" />
    <SingelCard
      @wasClicked="changeActive(index)"
      @showDelete="showDelete(index)"
      @hideDelete="hideDelete(index)"
      :card="card"
      v-else
      v-for="(card, index) in savedCardsArray"
      :key="card.index"
      :class="{ active: index === 0 }"
      :style="{ zIndex: index }"
    />
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
      deleteBtn: false,
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
    showConfirm() {
      if (this.confirmView === true) {
        this.confirmView = false;
      } else {
        this.confirmView = true;
      }
    },
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
.delete-btn {
  min-width: 200px;
  padding: 0px;
}

.single-card:not(:first-of-type):hover {
  transform: translateY(-20%);
}

.single-card:not(:first-of-type) {
  position: relative;
  margin-bottom: -180px;
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
.full-btn {
  margin-top: 210px;
}
.empty-btn {
  margin-top: 80px;
}
</style>
