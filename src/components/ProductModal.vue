<!--Компонент расширенной карточки товара-->
<template>
    <div class="modal"
         style="display:block !important" tabindex="-1" role="dialog">
        <div class="modal-dialog" role="document">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">Карточка товара</h5>
                    <button @click="hideModal" type="button" class="close" data-dismiss="modal" aria-label="Close">
                        <span aria-hidden="true">&times;</span>
                    </button>
                </div>
                <div class="modal-body">
                    <div class="col-10 pl-1">
                        <div class="card text-center border-0 shadow-sm mb-3 bg-white rounded-lg">
                            <img class="card-img-top" v-bind:src="product.img"
                            >
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
                            </div>
                        </div>
                    </div>
                </div>
                <div class="modal-footer">
                    <button @click="buyProduct" type="button" class="btn btn-primary">Купить</button>
                    <button @click="hideModal" type="button" class="btn btn-secondary" data-dismiss="modal">Закрыть
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "Product",
        props: {
            product: {
                type: Object,
                required: true
            }
        },
        methods: {
            //Метод для "покупки" товара
            buyProduct() {
                alert(`Куплен товар ${this.product.name}`)
                this.hideModal()
            },
            //Метод для сокрытия карточки товара, эмитит view Products
            hideModal() {
                this.$emit('hide-modal')
            }
        }
    }
</script>

<style scoped>

</style>