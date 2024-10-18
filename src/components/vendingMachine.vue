<script setup>
</script>

<template>
  <div class="vendingMachine">
    <div class="wrapperContainer">
      <div class="itemWrapper">
        <div class="itemListWrapper">
          <div class="itemList">something</div>
        </div>
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
}

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

.itemListWrapper {
}
.itemList {
}
</style>
