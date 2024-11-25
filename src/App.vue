<script setup>
  import { ref, computed } from "vue";
  import ShoppingItem from "./components/ShoppingItem.vue";

  const newItem = ref("");
  const items = ref([]);

  const remainingItems = computed(() => items.value.filter(item => !item.isPurchased).length);

  function addItem() {
    if (newItem.value.trim()) {
      items.value.push({ name: newItem.value.trim(), isPurchased: false });
      newItem.value = "";
    }
  }

  function removeItem(index) {
    items.value.splice(index, 1); // Delete the item by index
  }

  function updateItem(index, updatedItem) {
    items.value[index] = updatedItem;
  }

  function togglePurchased(index) {
    items.value[index].isPurchased = !items.value[index].isPurchased; // Change the shopping status
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

    <p v-if="items.length > 0" class="remaining-message">
      You have {{ remainingItems }} items left to buy.
    </p>

    <p v-if="items.length === 0" class="empty-message">Your shopping list is empty!</p>

    <ul v-show="items.length > 0">
      <ShoppingItem
        v-for="(item, index) in items"
        :key="index"
        :item="item"
        @togglePurchased="togglePurchased(index)"
        @updateItem="updatedItem => updateItem(index, updatedItem)"
        @remove="removeItem(index)"
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

  .remaining-message {
    color: #007bff; /* Azul llamativo */
    font-weight: bold;
    margin: 20px 0;
  }

</style>
