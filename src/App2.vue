<script setup>
import { onMounted, ref } from "vue"; // if compared to REACTJS - it is something like useState

const name = ref("albert");
const status = ref(true);
const task = ref(["one", "two", "three"]);

const deleteTask = (itemIndex) => {
  task.value.splice(itemIndex, 1);
};

// whenever the template is mounted on the DOM
onMounted(async () => {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/todos");
    const data = await response.json();

    console.log(data);

    task.value = data.map((item) => item.title);
  } catch (err) {
    console.log(err);
  }
});
</script>

<template>
  <div>
    <h1>{{ name }}</h1>
    <p v-if="status">status is active</p>
    <h3>Tasks:</h3>
    <ul>
      <li v-for="(t, index) in task" :key="t">
        <span style="margin-right: 5px">{{ t }}</span>
        <button @click="deleteTask(index)">X</button>
      </li>
    </ul>
  </div>
</template>

<!-- scoped : it will just reference every h1 in this particular component -->
<!-- <style scoped>
h1 {
  color: red;
}
</style> -->
