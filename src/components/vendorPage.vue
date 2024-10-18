<script setup>
import { ref } from "vue";
import Keyboard from "./keyboard.vue";
import VendingMachine from "./vendingMachine.vue";

const vendingItems = ref([
  {
    itemTitle: "one",
    itemNo: 1,
    itemPrice: 1,
  },
  {
    itemTitle: "two",
    itemNo: 2,
    itemPrice: 2,
  },
  {
    itemTitle: "three",
    itemNo: 3,
    itemPrice: 3,
  },
]);
</script>
<template>
  <div class="vendorPage">
    <div class="vendingContainer">
      <VendingMachine :vendingItems="vendingItems" />
    </div>
    <div class="keyContainer">
      <Keyboard :vendingItems="vendingItems" />
    </div>
  </div>
</template>

<style scoped lang="scss">
.vendorPage {
  height: 100vh;
  display: grid;
  grid-template-columns: 1.5fr 1fr;

  @media (max-width: 768px) {
    grid-template-columns: 1fr;
  }
}

.keyContainer {
  padding: 0 5em;

  @media (max-width: 992px) {
    padding: 1em 3em;
  }

  @media (max-width: 576px) {
    padding: 0em 1em;
  }
}
</style>
