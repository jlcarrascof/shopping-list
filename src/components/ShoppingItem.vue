<script setup>
    import { defineProps } from 'vue';

    const props = defineProps({
        item: String
    });
</script>

<template>
    <li class="shopping-item">
        {{ item }}
        <button @click="removeItem">Eliminar</button>
    </li>
</template>

<style scoped>
    .shopping-item {
        padding: 8px;
        background-color: #f9f9f9;
        border: 1px solid #ddd;
        margin-bottom: 5px;
        border-radius: 5px;
    }
</style>
