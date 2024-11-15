<script setup>
    const props = defineProps({
        item: String
    });

    const emit = defineEmits();

    function removeItem() {
        emit('remove', props.item); // Emit the 'remove' event
    }

</script>

<template>
    <li class="shopping-item">
        {{ item }}
        <button @click="removeItem">Eliminar</button>
    </li>
</template>

<style scoped>
    .shopping-item {
        display: flex;
        justify-content: space-between;
        padding: 8px;
        background-color: #f9f9f9;
        border: 1px solid #ddd;
        margin-bottom: 5px;
        border-radius: 5px;
    }
</style>
