<script setup>

    import { ref, watch } from 'vue';

    const props = defineProps({
        item: Object, // kind of: { name, isPurchased}
    });

    const emit = defineEmits(['updateItem', 'togglePurchased', 'remove']);

    const isEditing = ref(false);
    const editedItem = ref(props.item.name);

    watch(
        () => props.item.name,
        (newVal) => {
            editedItem.value = newVal;
        }
    );


    function toggleEditMode() {
        if (isEditing.value) {
            emit('updateItem', { ...props.item, name: editedItem.value });
        }
        isEditing.value = !isEditing.value;
    }

    function togglePurchased() {
        emit('togglePurchased');
    }
</script>

<template>
    <li class="shopping-item"
        :class="{ purchased: item.isPurchased}"
        @click.stop="togglePurchased"
    >
        <span v-if="!isEditing">{{ item.name }}</span>
        <input v-model="editedItem" v-if="isEditing" type="text" />
        <div class="buttons-container">
            <button @click.stop="toggleEditMode" class="edit-btn">
            {{ isEditing ? 'Guardar' : 'Editar' }}
            </button>
            <button @click.stop="$emit('remove')" class="delete-btn">Delete</button>
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

    .shopping-item.purchased {
        text-decoration: line-through;
        color: #6c757d;
        background-color: #e9ecef;
    }

    button {
        color: white;
        border: none;
        border-radius: 5px;
        padding: 4px 8px;
        cursor: pointer;
    }

    .buttons-container {
        display: flex;
        gap: 8px;
    }

    button.edit-btn {
        background-color: #007bff;
    }

    button.edit-btn:hover {
        background-color: #0056b3;
    }

    button.edit-btn.is-saving {
        background-color: #28a745;
    }

    button.delete-btn {
        background-color: #ff4d4d;
    }

    button.delete-btn:hover {
        background-color: #d11a2a;
    }
</style>
