<template>
  <div class="add-card-view">
    <h1>Add A New Bank Card</h1>
    <p :style="{ color: 'darkgrey' }">New card</p>
    <NewCardForm @viewChange="$emit('viewChange')" />
  </div>
</template>

<script>
import { NewCardForm } from "../components";
export default {
  methods: {},

  components: { NewCardForm },
};
</script>

<style></style>
