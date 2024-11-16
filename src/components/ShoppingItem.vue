<script setup>
    const props = defineProps({
        item: String
    });

    // const emit = defineEmits();

    // control Edition mode
    const isEditing = ref(false);
    // copy the item to be modified
    const editedItem = ref(props.item);

    function toggleEditMode() {
         if (isEditing.value) {
            // If we are saving, emit changes.
            $emit('updateItem', editedItem.value);
    }

    isEditing.value = !isEditing.value; // Alternate the mode.
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
