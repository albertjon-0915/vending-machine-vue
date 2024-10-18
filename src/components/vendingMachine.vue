<script setup>
import { defineProps, ref } from "vue";

const props = defineProps({
  vendingItems: Array,
});

const itemList = ref([...props.vendingItems]);
</script>

<template>
  <div class="vendingMachine">
    <div class="wrapperContainer">
      <div class="itemWrapper">
        <ul class="itemList">
          <li v-for="item in itemList" :key="item">
            <div>{{ item.itemTitle }}</div>
            <div>{{ item.itemPrice }}</div>
            <div>{{ item.itemNo }}</div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.vendingMachine {
  display: grid;
  place-items: center;
  height: 100vh;
  padding: 1em 3em;

  .wrapperContainer {
    width: 95%;
    height: 100%;
    background: #eeeeee;

    border-radius: 5px;
    display: flex;
    justify-content: end;
    padding: 2em;

    .itemWrapper {
      border-radius: 15px;
      max-width: 90%;
      min-width: 45vw;
      height: 100%;
      background: #dddddd;
    }
  }
}

.itemList {
  display: flex;

  li {
    all: unset;
  }
}
</style>
