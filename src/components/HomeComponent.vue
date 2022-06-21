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
                :total-amount="totalAmount"
            >
                <template #graphic>
                    <Graphic
                        :amounts="amountsGraphic"
                        @tap-select="tapSelect"
                    ></Graphic>
                </template>
                <template #action>
                    <ActionComponent 
                        @create-movement="createMovement"
                    />
                </template>
            </Resume>
            
        </template>
        <template #movements>
            <Movements
                :movements="movements"
                @remove-movement="removeMovement"
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
            movements:[], 
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
                const lastMovements = last30Days.slice(0, i + 1);
                return lastMovements.reduce((sum, movement) =>{
                    return sum + movement
                }, 0)
            })
        }, 
        totalAmount() {
            return this.movements.reduce((totalSum, movement) => {
                return totalSum + movement.amount
            }, 0)
        }
    },
    mounted() {
        const getMovements = JSON.parse(localStorage.getItem('new-movements'))

        if(Array.isArray(getMovements)) {
            this.movements = getMovements?.map(mov => {
                return { ...mov, time: new Date(mov.time)}
            });
        } 
    },
    methods: {
        createMovement(movFromAction) {
            this.movements.push(movFromAction);
            this.saveMovement()
        },
        removeMovement(id) {
            const index = this.movements.findIndex(eachMov => eachMov.id === id);
            this.movements.splice(index, 1);
            this.saveMovement()
        },
        saveMovement() {
            localStorage.setItem('new-movements', JSON.stringify(this.movements))
        },
        tapSelect(el) {
            console.log(el)
            this.amount = el;
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