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
                <template #graphic>
                    <Graphic
                        :amounts="amountsGraphic"
                    ></Graphic>
                </template>
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
import Graphic from './Resume/Graphic.vue'

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
                    amount: 1000,
                    time: new Date('06-20-2022')
                },
                {
                    id: 1,
                    title: "Movimiento 2",
                    description: "Lorem ipsum dolor sit amet.",
                    amount: 2000,
                    time: new Date('05-20-2022')
                },
                {
                    id: 2,
                    title: "Movimiento 3",
                    description: "Lorem ipsum dolor sit amet.",
                    amount: -4000,
                    time: new Date('06-20-2022')
                },
                {
                    id: 3,
                    title: "Movimiento 4",
                    description: "Lorem ipsum dolor sit amet.",
                    amount: 4000,
                    time: new Date('06-20-2022')
                },
                {
                    id: 4,
                    title: "Movimiento 5",
                    description: "Lorem ipsum dolor sit amet.",
                    amount: -500,
                    time: new Date('05-20-2022')
                },
                {
                    id: 5,
                    title: "Movimiento 6",
                    description: "Lorem ipsum dolor sit amet.",
                    amount: 6000,
                    time: new Date('01-20-2022')
                },
                {
                    id: 6,
                    title: "Movimiento 7",
                    description: "Lorem ipsum dolor sit amet.",
                    amount: 7000,
                    time: new Date('03-20-2022')
                },
                {
                    id: 7,
                    title: "Movimiento 8",
                    description: "Lorem ipsum dolor sit amet.",
                    amount: 8000,
                    time: new Date('06-20-2022')
                },
            ], 
        }
    },
    computed: {
        amountsGraphic() {
            const last30Days = this.movements.filter(mov => {
                const today = new Date();
                const oldDate = today.setDate(today.getDate() - 30)

                return mov.time >= oldDate
            }).map(mov => mov.amount)

            return last30Days.map((m, i) => {
                const previousMovements = last30Days.slice(0, i);
                return previousMovements.reduce((suma, movement) =>{
                    return suma + movement
                }, 0)
            })
        }
    },
    components: {
        LayoutComponent,
        HeaderComponent,
        Resume,
        Movements,
        ActionComponent,
        Graphic
    }
}
</script>