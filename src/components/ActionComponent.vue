<template>
    <button @click="showModal = true">Agregar movimiento</button>
    <Teleport to="#app">
        <Modal v-show="showModal" @close-modal="showModal = false">
            <form @submit.prevent="submit">
                <div class="field">
                    <label>Título del movimiento</label>
                    <input type="text" v-model="title"/>
                </div>
                <div class="field">
                    <label>Monto</label>
                    <input type="number" v-model="amount" />
                </div>
                <div class="field">
                    <label>Descripción</label>
                    <textarea rows="4" v-model="description"></textarea>
                </div>
                <div class="field">
                    <label>Tipo de movimiento</label>
                    <label class="radio-label">
                        <input type="radio" value="Ingreso" v-model="movementType"/>
                        <span>Ingreso</span>
                    </label>
                    <label class="radio-label">
                        <input type="radio" value="Gasto" v-model="movementType"/>
                        <span>Gasto</span>
                    </label>
                </div>
                <div class="action">
                    <button>Agregar movimiento</button>
                </div>
            </form>
        </Modal>
    </Teleport>
</template>

<script setup>
import { ref, defineEmits } from "vue";

import Modal from "./Modal.vue";

const showModal = ref(false);

const title = ref(""); 

const amount = ref(0);

const description = ref("");

const movementType = ref("Ingreso");

const emit = defineEmits(['create-movement'])

const submit = () => {
    showModal.value = !showModal.value;
    emit('create-movement', {
      id: new Date().getTime(),
      title: title.value,
      description: description.value,
      amount: movementType.value === "Ingreso" ? amount.value : -amount.value, 
      time: new Date(), 
    })
    title.value = ""
    description.value = ""
    amount.value = 0
    movementType.value = "Ingreso"

}

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
    margin-block-end: 12px;
}
form {
  font-size: 1.24rem;
  width: 100%;
}
form .action {
  padding: 0 24px;
}
.field {
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  padding: 16px 24px;
}
label {
  margin-bottom: 8px;
}
input,
textarea {
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
  margin-top: 8px;
}
.radio-label span {
  margin-top: 4px;
  margin-left: 8px;
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