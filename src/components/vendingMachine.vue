<script setup>
import { defineProps, ref } from "vue";

// get props from parent
const props = defineProps({
  vendingItems: Array,
});

const itemList = ref([...props.vendingItems]);
</script>

<!-- Display vending machine -->
<template>
  <div class="vendingMachine">
    <div class="wrapperContainer">
      <div class="itemWrapper">
        <ul class="itemList">
          <li v-for="item in itemList" :key="item">
            <img :src="item.itemImg" alt="img" />
            <h2>{{ item.itemTitle }}</h2>
            <div class="bill">Php {{ item.itemPrice }}</div>
            <div class="itemNumber">{{ item.itemNo }}</div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
$vendingM-bg-pr-color: #eeeeee;
$vendingM-bg-sc-color: #dddddd;
$pesoBill-bg-color: #68ad00;
$border-bgPrice-color: #808080;
$secondary-bg-color: #07ebdca1;

// =================== Containers =================== //
.vendingMachine {
  display: grid;
  place-items: center;
  height: 100vh;
  padding: clamp(0em, 1vw, 1em) clamp(0em, 2vw, 2em);

  .wrapperContainer {
    $padding-small: clamp(1em, 2vw, 2em);
    $padding-large: clamp(2em, 7vw, 7em);

    width: 95%;
    height: 100%;
    background: $vendingM-bg-pr-color;
    border-radius: 5px;
    display: flex;
    justify-content: end;

    padding-left: $padding-small;
    padding-right: $padding-small;
    padding-top: $padding-small;
    padding-bottom: $padding-small;

    .itemWrapper {
      border-radius: 15px;
      max-width: 90%;
      min-width: 45vw;
      width: 100%;
      height: 100%;
      background: $vendingM-bg-sc-color;
    }
  }
}

// ============== vendingMachine Items =============== //
.itemList {
  display: flex;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  place-items: center;
  height: 100vh;
  overflow-x: hidden;
  overflow-y: auto;
  padding: 0.5em;
  gap: 1em;

  &::-webkit-scrollbar {
    width: 0.5em;
  }

  &::-webkit-scrollbar-track {
    margin-block: 0.9em;
  }

  &::-webkit-scrollbar-thumb {
    background: lighten($border-bgPrice-color, 15%);
    border-radius: 5px;

    &:hover {
      background: $border-bgPrice-color;
    }
  }

  li {
    all: unset;
    position: relative;
    display: flex;
    justify-content: flex-end;
    align-items: center;
    flex-direction: column;

    aspect-ratio: 1 / 1;
    width: clamp(5em, 12vw, 15em);
    padding: 0.5em 0;
    border-radius: 10px;
    border: 1px solid lighten($border-bgPrice-color, 25%);

    .itemNumber {
      margin: 0.5em 0;
      padding: 0.5em clamp(1.5em, 2.5vw, 3em);
      border-radius: 50%;
      border: 1px solid $border-bgPrice-color;
      background: radial-gradient(
        circle at center,
        lighten($border-bgPrice-color, 15%),
        $border-bgPrice-color
      );
      color: $vendingM-bg-pr-color;
      font-weight: 900;
    }

    .bill {
      font-size: 1.2em;
      font-weight: 700;
      color: $pesoBill-bg-color;
    }

    img {
      filter: grayscale(0.6);
      box-shadow: -2px 1px 10px 1px $secondary-bg-color;
      border-radius: 50%;
      width: clamp(3em, 6vw, 6em);
      aspect-ratio: 1 / 1;
    }

    h2 {
      margin-bottom: clamp(0.5em, 1vw, 1em);
    }
  }
}

// ================ media queries ================ //
@media (max-width: 1200px) {
  .vendingMachine {
    height: 70vh;
    padding: 3em 0;
  }

  .itemList {
    height: 70vh;
    grid-template-columns: repeat(2, 1fr);
    gap: 2em;

    li {
      padding: 0.5em 2em;
    }
  }
}
@media (max-width: 992px) {
}
@media (max-width: 768px) {
  .vendingMachine {
    height: 50vh;
    padding: 0;
  }

  .itemList {
    height: 50vh;
    grid-template-columns: repeat(3, 1fr);
    gap: 1em;
  }
}
@media (max-width: 576px) {
  .itemList {
    grid-template-columns: repeat(2, 1fr);
    gap: 0.5em;

    li {
      padding: 0.5em 1.5em;
    }
  }
}
</style>
