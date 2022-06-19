<template>
    <div>
        <p>{{ labelVisual }}</p>
        <h1>{{ amountCurrency }}</h1>
        <article class="graphic">
            <slot name="graphic"></slot>
        </article>
        <article class="action">
            <slot name="action"></slot>
        </article>
    </div>
</template>

<script>

const currencyFormatter = new Intl.NumberFormat('es-CO', {
    style: "currency",
    currency: "COP",
})

export default {
    props: {
        label: {
            type: String,
        },
        specificDate : {
            type: String, 
        },
        amount: {
            type: Number, 
            default: null, 
        },
        totalAmount: {
            type: Number, 
        } 
    }, 
    computed: {
        labelVisual() {
            return this.label !== null ? this.label : this.specificDate;
        },
        amountVisual() {
            return this.amount !== null ? this.amount : this.totalAmount;
        },
        amountCurrency() {
            return currencyFormatter.format(this.amountVisual); 
        }
    }
}

</script>

<style scoped>
main {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    width: 100%;
}

h1, p {
    margin: 0;
    text-align: center;
}

h1 {
    margin-block-start: 14px;
    color: var(--brand-green)
}

.graphic {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    padding: 48px 24px;
    box-sizing: border-box;
}
</style>