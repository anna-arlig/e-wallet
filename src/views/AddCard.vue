<template>
  <div class="add-card-view">
    <h1>Add A New Bank Card</h1>
    <p>New card</p>
    <NewCardForm @viewChange="$emit('viewChange')" @send="$emit('send')" />
  </div>
</template>

<script>
import { NewCardForm } from "../components";
export default {
  methods: {
    clickAdd() {
      return this.$emit("viewChange");
    },
  },
  components: { NewCardForm },
};
</script>

<style></style>
