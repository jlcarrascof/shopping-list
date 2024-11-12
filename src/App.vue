<script setup>
  import { ref } from "vue";

  const newItem = ref("");

  function addItem() {
    console.log(`Product Added: ${newItem.value}`);
    newItem.value = "";
  }

</script>

<template>
  <div id="app">
    <h1>Welcome to your shopping list app!</h1>
    <p>Let's add some products</p>

    <input
      type="text"
      v-model="newItem"
      placeholder="Write a product description"
    />

    <button @click="addItem">Add</button>

  </div>
</template>

<style scoped>
  #app {
    text-align: center;
    font-family: Arial, Helvetica, sans-serif;
    max-width: 600px;
    margin: auto;
    color: #333;
  }
</style>
