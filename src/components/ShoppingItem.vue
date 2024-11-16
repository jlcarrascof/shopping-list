<script setup>

    import { ref, watch } from 'vue'; // Importamos watch para observar cambios

    const props = defineProps({
        item: String,
    });

    const emit = defineEmits(['updateItem', 'remove']); // Define los eventos

    const isEditing = ref(false); // Controla el modo de edición
    const editedItem = ref(props.item); // Crea una copia editable del artículo

    watch(
        () => props.item,
        (newVal) => {
            editedItem.value = newVal; // Sincroniza editedItem con el valor actual de item
        }
    );


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
        <div class="buttons-container">
            <button @click="toggleEditMode" class="edit-btn">
            {{ isEditing ? 'Guardar' : 'Editar' }}
            </button>
            <button @click="$emit('remove', item)" class="delete-btn">Delete</button>
        </div>
    </li>
</template>

<style scoped>
    .shopping-item {
        display: flex;
        justify-content: space-between;
        align-items: center;
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

    .buttons-container {
        display: flex; /* Alinea los botones horizontalmente */
        gap: 8px; /* Añade espacio entre los botones */
    }

    button.edit-btn {
        background-color: #007bff; /* Azul para Editar */
    }

    button.edit-btn:hover {
        background-color: #0056b3; /* Azul más oscuro para hover */
    }

    button.edit-btn.is-saving {
        background-color: #28a745; /* Verde para Guardar */
    }

    button.delete-btn {
        background-color: #ff4d4d;
    }
</style>
