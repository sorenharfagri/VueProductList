<template>
    <div class="col-6 pl-2">
        <div @click="showModal"
             style="cursor: pointer"
             class="card text-center border-0 shadow-sm mb-3 bg-white rounded-lg">
            <img class="card-img-top"
                 v-bind:src="product.img">
            <div class="card-body p-1 m-1">
                <h5 class="card-title mb-0">{{product.name}}</h5>
                <div class="card-text">
                    <div>
                        <small class="card-text text-muted">
                            Категория: {{product.category}}
                        </small>
                    </div>
                    <div>
                        <del class="m-1">{{product.oldPrice}}</del>
                        <strong>{{product.price}} ₽</strong>
                    </div>
                    <div class="alert alert-dark p-0 m-0" role="alert">
                        <div>
                            <small>
                                <strong>Бренд</strong> {{product.brand}}
                            </small>
                        </div>
                        <div>
                            <small>
                                <strong>Размер</strong> {{product.size}}
                            </small>
                        </div>
                        <div>
                            <small>
                                <strong>Цвет</strong> {{product.color}}
                            </small>
                        </div>
                    </div>
                </div>
                <button @click.stop="buyProduct" class="btn btn-primary m-1">Купить</button>
            </div>
        </div>
    </div>
</template>

<script>

    export default {
        name: "Product",
        data() {
            return {
                visible: false
            }
        },
        props: {
            product: {
                type: Object,
                required: true
            }
        },
        methods: {
            buyProduct() {
                alert(`Куплен товар ${this.product.name}`)
            },
            showModal() {
                this.$emit('show-modal', this.product.id)
            }
        }
    }
</script>

<style scoped>

</style>

<!--                        @click.prevent="buyProduct"-->