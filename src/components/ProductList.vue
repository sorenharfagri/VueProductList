<template>
    <div>
        <div class="alert alert-light" role="alert">
            Найдено {{products.length}} товара
        </div>
        <div class="row no-gutters">
            <Product
                    v-for="product of products"
                    :key="product.id"
                    v-bind:product="product"
                    @show-modal="showModal"
            />
        </div>
    </div>
</template>

<script>

    import Product from '@/components/Product'
    export default {
        name: "ProductList",
        props: {
            products: {
                type: Array
            }
        },
        components: {
            Product
        },
        methods: {
            showModal(id) {
                this.$emit('show-modal', id)
            }
        }
    }
</script>