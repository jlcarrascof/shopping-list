<script setup>
  import { ref } from "vue";
  import ShoppingItem from "./components/ShoppingItem.vue";

  const newItem = ref("");
  const items = ref([]);

  function addItem() {
    if (newItem.value.trim()) {
      items.value.push(newItem.value.trim());
      newItem.value = "";
    }
  }

  function removeItem(itemToRemove) {
    items.value = items.value.filter(item => item !== itemToRemove);
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

    <p v-if="items.length === 0" class="empty-message">Your shopping list is empty!</p>

    <ul v-show="items.length > 0">
      <ShoppingItem
        v-for="(item, index) in items"
        :key="index"
        :item="item"
        @updateItem="updateItem(index)"
        @remove="removeItem"
      />

    </ul>

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

  input {
    padding: 8px;
    font-size: 16px;
    width: calc(100% - 20px);
    margin-bottom: 10px;
  }

  button {
    padding: 8px 20px;
    font-size: 16px;
    cursor: pointer;
    background-color: #4CAF50;
    color: white;
    border: none;
    border-radius: 5px;
  }

  ul {
    list-style-type: none;
    padding: 0;
    margin-top: 20px;
  }

 .empty-message {
    color: red;
    font-style: italic;
  }

</style>
