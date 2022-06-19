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
                <template #action>Action</template>
            </Resume>
            
        </template>
        <template #movements>
            <Movements></Movements>
        </template>
    </LayoutComponent>
</template>

<script>
import LayoutComponent from './LayoutComponent.vue'
import HeaderComponent from './HeaderComponent.vue'
import Resume from './Resume/Index.vue'
import Movements from './Movements.vue'

export default {
    data() {
        return {
            amount: null, 
            specificDate: null, 
        }
    },
    components: {
        LayoutComponent,
        HeaderComponent,
        Resume,
        Movements
}
}
</script>