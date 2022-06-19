<template>
    <button @click="showModal = true">Agregar movimiento</button>
    <Teleport to="#app">
        <Modal v-show="showModal" @close-modal="showModal = false">Modal</Modal>
    </Teleport>
</template>

<script setup>
import { ref } from "vue";

import Modal from "./Modal.vue";

const showModal = ref(false);
</script>

<style scoped>
button {
    color: white;
    font-size: .8rem;
    font-family: 'system-ui', sans-serif ;
    font-weight: 600;
    letter-spacing: .07rem;
    text-transform: uppercase;
    background-color: var(--brand-blue);
    border: none;
    width: 100%;
    padding: 12px 36px;
    border-radius: 60px;
    box-sizing: border-box;
}

form {
    font-size: 1.24rem;
    width: 100%;
}

input, textarea {
    font-size: 1.24rem;
    border: 2px solid var(--brand-blue);
    border-radius: 8px;
    padding: 8px;
}
input[type="number"] {
    text-align: right;
}
.radio-label {
    display: flex;
    align-items: center;
    margin-block-start: 8px;
}
.radio-label span {
    margin-block-start: 4px;
    margin-inline-start: 8px;
}
input[type="radio"] {
    appearance: none;
    width: 1.24rem;
    height: 1.24rem;
    color: var(--brand-blue);
    border: 2px solid var(--brand-blue);
    border-radius: 50%;
}

input[type="radio"]:checked {
    background-color: var(--brand-blue);
}
</style>