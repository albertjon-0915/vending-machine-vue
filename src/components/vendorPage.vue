<script setup>
import { ref } from "vue";
import Keyboard from "./keyboard.vue";
import VendingMachine from "./vendingMachine.vue";
import VendingMachineLogo from "../assets/vendingMachine.jpg";

// mock vending machine item list
const vendingItems = ref([
  { itemImg: VendingMachineLogo, itemTitle: "Lays", itemNo: 1, itemPrice: 1 },
  {
    itemImg: VendingMachineLogo,
    itemTitle: "Doritos",
    itemNo: 2,
    itemPrice: 600,
  },
  {
    itemImg: VendingMachineLogo,
    itemTitle: "Snickers",
    itemNo: 3,
    itemPrice: 27,
  },
  {
    itemImg: VendingMachineLogo,
    itemTitle: "KitKat",
    itemNo: 4,
    itemPrice: 12,
  },
  { itemImg: VendingMachineLogo, itemTitle: "Twix", itemNo: 5, itemPrice: 23 },
  {
    itemImg: VendingMachineLogo,
    itemTitle: "Pringles",
    itemNo: 6,
    itemPrice: 45,
  },
  { itemImg: VendingMachineLogo, itemTitle: "Oreo", itemNo: 7, itemPrice: 87 },
  { itemImg: VendingMachineLogo, itemTitle: "M&Ms", itemNo: 8, itemPrice: 132 },
  {
    itemImg: VendingMachineLogo,
    itemTitle: "Skittles",
    itemNo: 9,
    itemPrice: 70,
  },
  {
    itemImg: VendingMachineLogo,
    itemTitle: "Milky Way",
    itemNo: 10,
    itemPrice: 99,
  },
  {
    itemImg: VendingMachineLogo,
    itemTitle: "Reese's",
    itemNo: 11,
    itemPrice: 43,
  },
  {
    itemImg: VendingMachineLogo,
    itemTitle: "Cheetos",
    itemNo: 12,
    itemPrice: 28,
  },
  {
    itemImg: VendingMachineLogo,
    itemTitle: "Ruffles",
    itemNo: 13,
    itemPrice: 300,
  },
  {
    itemImg: VendingMachineLogo,
    itemTitle: "Fritos",
    itemNo: 14,
    itemPrice: 65,
  },
  {
    itemImg: VendingMachineLogo,
    itemTitle: "Pop-Tarts",
    itemNo: 15,
    itemPrice: 49,
  },
  {
    itemImg: VendingMachineLogo,
    itemTitle: "SunChips",
    itemNo: 16,
    itemPrice: 120,
  },
  {
    itemImg: VendingMachineLogo,
    itemTitle: "Tostitos",
    itemNo: 17,
    itemPrice: 510,
  },
  {
    itemImg: VendingMachineLogo,
    itemTitle: "Planters",
    itemNo: 18,
    itemPrice: 30,
  },
  {
    itemImg: VendingMachineLogo,
    itemTitle: "Welch's",
    itemNo: 19,
    itemPrice: 92,
  },
  {
    itemImg: VendingMachineLogo,
    itemTitle: "Nature Valley",
    itemNo: 20,
    itemPrice: 135,
  },
  {
    itemImg: VendingMachineLogo,
    itemTitle: "Triscuit",
    itemNo: 21,
    itemPrice: 240,
  },
  {
    itemImg: VendingMachineLogo,
    itemTitle: "Cheez-It",
    itemNo: 22,
    itemPrice: 160,
  },
  {
    itemImg: VendingMachineLogo,
    itemTitle: "Clif Bar",
    itemNo: 23,
    itemPrice: 83,
  },
  {
    itemImg: VendingMachineLogo,
    itemTitle: "Goldfish",
    itemNo: 24,
    itemPrice: 76,
  },
  { itemImg: VendingMachineLogo, itemTitle: "Ritz", itemNo: 25, itemPrice: 60 },
  {
    itemImg: VendingMachineLogo,
    itemTitle: "Gushers",
    itemNo: 26,
    itemPrice: 180,
  },
  {
    itemImg: VendingMachineLogo,
    itemTitle: "Combos",
    itemNo: 27,
    itemPrice: 250,
  },
  {
    itemImg: VendingMachineLogo,
    itemTitle: "Fruit Roll-Ups",
    itemNo: 28,
    itemPrice: 110,
  },
  {
    itemImg: VendingMachineLogo,
    itemTitle: "Teddy Grahams",
    itemNo: 29,
    itemPrice: 40,
  },
  {
    itemImg: VendingMachineLogo,
    itemTitle: "Cracker Jack",
    itemNo: 30,
    itemPrice: 67,
  },
]);
</script>

<!-- Vending machine page -->
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
