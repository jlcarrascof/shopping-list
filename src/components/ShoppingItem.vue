<script setup>

    import { ref, watch } from 'vue'; // Importamos watch para observar cambios

    const props = defineProps({
        item: String,
    });

    const emit = defineEmits(['updateItem', 'remove']); // Define los eventos

    const isEditing = ref(false); // Controla el modo de edición
    const editedItem = ref(props.item); // Crea una copia editable del artículo

    function toggleEditMode() {
        if (isEditing.value) {
            emit('updateItem', editedItem.value); // Emitimos el artículo actualizado
        }
        isEditing.value = !isEditing.value; // Alternamos entre edición y visualización
    }
</script>

<template>
    <li class="shopping-item">
        <span v-if="!isEditing">{{ item }}</span>
        <input v-model="editedItem" v-if="isEditing" type="text" />
        <button @click="toggleEditMode">
            {{ isEditing ? 'Guardar' : 'Editar' }}
        </button>
        <button @click="$emit('remove', item)" class="delete-btn">Delete</button>
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

    button {
        color: white;
        border: none;
        border-radius: 5px;
        padding: 4px 8px;
        cursor: pointer;
    }

    button.delete-btn {
        background-color: #ff4d4d;
    }
</style>
