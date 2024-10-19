<script setup>
import VendorPage from "./components/vendorPage.vue";
</script>

<!-- Main page -->
<template>
  <div>
    <div class="titleSection">
      <div class="titleWrapper">
        <span>Vending Machine</span>
        <p>
          The Vending Machine project is a user-friendly Vue.js application that
          simulates a real vending machine. Users can easily input item numbers
          and view their selections through an intuitive interface.
        </p>
      </div>
    </div>

    <VendorPage />
  </div>
</template>

<style scoped lang="scss">
.titleSection {
  display: grid;
  place-items: center;

  .titleWrapper {
    display: flex;
    flex-direction: column;
    justify-content: center;
    width: 95%;
    height: clamp(12em, 15vw, 15em);
    margin: clamp(0.5em, 2vw, 2em);
    padding: 0 clamp(2em, 5vw, 5em);
    background: linear-gradient(120deg, #e9b7ce, #d3f3f1);
    border-radius: 15px;

    span {
      color: #000000;
      font-size: clamp(2.5em, 3.5vw, 3.5em);
      font-family: "Bungee", sans-serif;
    }

    p {
      max-width: clamp(30em, 50vw, 50em);
      font-size: clamp(0.8em, 1vw, 1em);
      color: #444444;
    }
  }
}
</style>
