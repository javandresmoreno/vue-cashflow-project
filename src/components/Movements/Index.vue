<template>
    <section class="movements">
        <h2 class="title">Historial</h2>
        <article class="content">
            <Movement 
                v-for="{ id, title, description, amount } in movements" 
                :key="id"
                :id="id"
                :title="title"
                :description="description"
                :amount="amount"
                @remove="remove"
            >
            </Movement>
        </article>
    </section>
</template>

<script setup>
import { defineProps, defineEmits, toRefs } from 'vue';

import Movement from './Movement.vue';

const props = defineProps({
    movements: {
        type: Array,
        default: () => [],
    }
})

const { movements } = toRefs(props)

const emit = defineEmits(['remove-movement'])

const remove = (id) => {
    emit('remove-movement', id)
    console.log("remove", id)
}

</script>

<style scoped>
    .movements{
        max-height: 100%;
        padding: 0 8px;
        margin-block-end: 14px;
    }
    .title {
        margin: 8px 16px 24px 16px;
        color: var(--brand-blue);
    }
    .content {
        max-height: 68vh;
        display: flex;
        flex-direction: column;
        gap: 8px;
        overflow-y: scroll;
    }
</style>