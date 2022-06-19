<template>
    <LayoutComponent>
        <template #header>
            <HeaderComponent></HeaderComponent>
        </template>
        <template #resume>
            <Resume></Resume>
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
    components: {
    LayoutComponent,
    HeaderComponent,
    Resume,
    Movements
}
}
</script>