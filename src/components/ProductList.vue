<!--Компонент является коллекцией компонентов Product-->
<!--Принимает массив товаров, затем их отображает-->

<template>
    <div>
        <div class="alert alert-light" role="alert">
            Найдено {{products.length}} товара
        </div>
        <div class="row no-gutters">
            <!--  show-modal - лисенер отображения расширенной карточки товара-->
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
            //Метод для отбражения расширенной краточки товара, эмитит view Products
            showModal(id) {
                this.$emit('show-modal', id)
            }
        }
    }
</script>