<template>
    <article>
        <svg
            @touchstart="tap" 
            @touchmove="tap"
            @touchend="untap"
            viewBox="0 0 300 200">
            <line 
                stroke="#c4c4c4" 
                stroke-width="1" 
                x1="0"
                :y1="zero"
                x2="300"
                :y2="zero"
            />
            <polyline 
                fill="none"
                stroke="#0689B0"
                stroke-width="1"
                :points="points"
            />
            <line
                v-show="showGreenPointer"
                stroke="#04B500" 
                stroke-width="1" 
                :x1="pointerCoordinates"
                y1="0"
                :x2="pointerCoordinates"
                y2="200"
            />
        </svg>
        <p>Últimos 30 días</p>
    </article>
</template>

<script setup>

import { defineProps, defineEmits, toRefs, computed, ref } from 'vue';

/* Props */

const props = defineProps({
    amounts: {
        type: Array, 
        default: () => []
    } 
})

/* Graphic Logic */

const { amounts } = toRefs(props)

const amountToPixels = (amount) => {
    const min = Math.min(...amounts.value);
    const max = Math.max(...amounts.value);

    const amountAbsolute = amount + Math.abs(min);
    const minmax = Math.abs(max) + Math.abs(min);

    return  200 - ((amountAbsolute * 100) / minmax) * 2 //el 200 digamos que invierte la grafica
}

const zero = computed(() => {
    return amountToPixels(0)
})

const points = computed(() => {
    const total = amounts.value.length;

    return amounts.value.reduce((points, amount, index) => {
        const x = (300 / total) * (index + 1);
        const y = amountToPixels(amount); 

        return `${points} ${x},${y}`;
    }, "0,100")
}) 

/* Tap events for green bar */

const showGreenPointer = ref(false)

const pointerCoordinates = ref(0)

const emit = defineEmits(["tap-select"])

const tap = ({ target, touches }) => {
    showGreenPointer.value = true;
    const elementWidth = target.getBoundingClientRect().width;
    const elementX = target.getBoundingClientRect().x;
    const touchX = touches[0].clientX;

    pointerCoordinates.value = (touchX - elementX) * 300 / elementWidth;

    emit("tap-select", amounts)
    console.log(emit)
}

const untap = () => {
    showGreenPointer.value = false;
}

</script>

<style scoped>

svg {
    width: 100%;
}

p {
    text-align: center;
}
</style>