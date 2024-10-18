<script setup>
import VendorPage from "./components/vendorPage.vue";
</script>

<template>
  <div>
    <div class="titleSection">
      <div class="titleWrapper">
        <span>Vending Machine</span>
        <p>
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Itaque
          inventore repellat nobis recusandae velit porro reiciendis quaerat
          excepturi nulla nisi.
        </p>
      </div>
    </div>

    <VendorPage />
  </div>
</template>

<!-- scoped : it will just reference every element(for example 'h1' in this component template) in this particular component -->
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
      // font: 3.5em "Bungee";
    }
    p {
      max-width: clamp(30em, 50vw, 50em);
      font-size: clamp(0.8em, 1vw, 1em);
      color: #444444;
    }
  }
}
</style>
