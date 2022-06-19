<template>
    <LayoutComponent>
        <template #header>
            <HeaderComponent></HeaderComponent>
        </template>
        <template #resume>
            <Resume 
                :label="'Ahorro Total'"
                :specific-date="specificDate"
                :amount="amount"
                :total-amount="1000000"
            >
                <template #graphic>Graphic</template>
                <template #action>
                    <ActionComponent></ActionComponent>
                </template>
            </Resume>
            
        </template>
        <template #movements>
            <Movements
                :movements="movements"
            >
            </Movements>
        </template>
    </LayoutComponent>
</template>

<script>
import LayoutComponent from './LayoutComponent.vue'
import HeaderComponent from './HeaderComponent.vue'
import Resume from './Resume/Index.vue'
import Movements from './Movements/Index.vue'
import ActionComponent from './ActionComponent.vue'

export default {
    data() {
        return {
            label: null, 
            amount: null,
            specificDate: null,
            movements:[
                {
                    id: 0,
                    title: "Movimiento 1",
                    description: "Lorem ipsum dolor sit amet.",
                    amount: 1000
                },
                {
                    id: 1,
                    title: "Movimiento 2",
                    description: "Lorem ipsum dolor sit amet.",
                    amount: 2000
                },
                {
                    id: 2,
                    title: "Movimiento 3",
                    description: "Lorem ipsum dolor sit amet.",
                    amount: -4000
                },
                {
                    id: 3,
                    title: "Movimiento 4",
                    description: "Lorem ipsum dolor sit amet.",
                    amount: 4000
                },
                {
                    id: 4,
                    title: "Movimiento 5",
                    description: "Lorem ipsum dolor sit amet.",
                    amount: -500
                },
                {
                    id: 5,
                    title: "Movimiento 6",
                    description: "Lorem ipsum dolor sit amet.",
                    amount: 6000
                },
                {
                    id: 6,
                    title: "Movimiento 7",
                    description: "Lorem ipsum dolor sit amet.",
                    amount: 7000
                },
                {
                    id: 7,
                    title: "Movimiento 8",
                    description: "Lorem ipsum dolor sit amet.",
                    amount: 8000
                },
            ], 
        }
    },
    components: {
    LayoutComponent,
    HeaderComponent,
    Resume,
    Movements,
    ActionComponent
}
}
</script>