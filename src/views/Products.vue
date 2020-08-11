<template>
    <div class="container-fluid">
        <h1>Список товаров</h1>
        <!--        Форма фильтрации-->
        <div class="row">
            <div class="col-12">
                <div class="card">
                    <div class="card-body">
                        <h5 class="card-title">Фильтры</h5>
                        <div class="card-text">
                            <form>
                                <div class="form-group">
                                    <select v-model="filter.brand" class="form-control">
                                        <option>Бренд</option>
                                        <option>Super</option>
                                        <option>Puper</option>
                                        <option>Cool</option>
                                        <option>Like</option>
                                    </select>
                                </div>
                                <div class="form-group">
                                    <select v-model="filter.size" class="form-control">
                                        <option>Размер</option>
                                        <option>29</option>
                                        <option>31</option>
                                        <option>35</option>
                                        <option>37</option>
                                        <option>42</option>
                                    </select>
                                </div>
                                <div class="form-group">
                                    <select v-model="filter.color" class="form-control">
                                        <option>Цвет</option>
                                        <option>Синий</option>
                                        <option>Красный</option>
                                        <option>Зеленый</option>
                                        <option>Белый</option>
                                        <option>Серый</option>
                                    </select>
                                </div>
                                <div class="text-right">
                                    <!--  Кнопка для сброса фильтров  -->
                                    <!--  Ссылается на статус isFiltered, который позволяет узнать, отсортированы ли товары  -->
                                    <!--  Если товары не отсортированы - кнопка не активна  -->
                                    <button
                                            :disabled='!filteredProducts.isFiltered'
                                            @click="removeFilters"
                                            class="btn btn-sm btn-secondary">Сбросить
                                    </button>
                                </div>
                            </form>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!--        Если товары имеются - отображаем их список-->
<!--        show-modal - Лисенер для отображения расширенной карточки товара-->
        <ProductList
                v-if="filteredProducts._products.length"
                v-bind:products="filteredProducts._products"
                @show-modal="showModal"
        />
<!--        Если товары не найдены - выводим соответствующее сообщение-->
        <div v-else class="alert alert-light" role="alert">Товары не найдены</div>
<!--        Расширенная карточка товара-->
<!--        ProductList имеет лисенер для её отображения-->
<!--        hide-modal - лисенер для сокрытия карточки-->
        <ProductModal
                v-if="productModalWindow.show"
                v-bind:product="products[productModalWindow.id]"
                @hide-modal="hideModal"
        />
    </div>
</template>

<script>
    import ProductList from '@/components/ProductList'
    import ProductModal from '@/components/ProductModal'

    export default {
        name: 'Products',
        components: {
            ProductList, ProductModal
        },
        data() {
            return {
                // Свойство, отвечающее за отображение расширенной карточки товара
                // show - отвечает за отображение карточки
                // id - хранит id товара, который необходимо отобразить в карточке
                productModalWindow: {
                    show: false,
                    id: ""
                },
                // Filter отвечает за фильтрацию, содержит её параметры
                // По умолчанию содержит названия категорий, в таком случае, фильтрации не происходит
                // Моделью связан с селектом формы фильтров
                filter: {
                    brand: "Бренд",
                    size: "Размер",
                    color: "Цвет"
                },
                //Список товаров
                products: [
                    {
                        id: 1,
                        name: 'Куртка красная',
                        img: 'https://media.istockphoto.com/photos/male-coat-isolated-on-the-white-picture-id163208487',
                        category: 'Куртки',
                        oldPrice: 5880,
                        price: 4790,
                        brand: 'Super',
                        size: 31,
                        color: 'Красный'
                    },
                    {
                        id: 2,
                        name: 'Куртка большая',
                        img: 'https://media.istockphoto.com/photos/red-womans-sports-jacket-picture-id520887025',
                        category: 'Куртки',
                        oldPrice: 5900,
                        price: 3790,
                        brand: 'Super',
                        size: 42,
                        color: 'Зеленый'
                    },
                    {
                        id: 3,
                        name: 'Куртка модная',
                        img: 'https://media.istockphoto.com/photos/male-coat-isolated-on-the-white-picture-id163208487',
                        category: 'Куртки',
                        price: 5550,
                        brand: 'Puper',
                        size: 29,
                        color: 'Красный'
                    },
                    {
                        id: 4,
                        name: 'Куртка выгодная',
                        img: 'https://media.istockphoto.com/photos/red-womans-sports-jacket-picture-id520887025',
                        category: 'Куртки',
                        oldPrice: 7900,
                        price: 1990,
                        brand: 'Super',
                        size: 29,
                        color: 'Зеленый'
                    }
                ],
            }
        },
        computed: {
            //Отфильтрованные товары
            //@return:
            //_products: []
            //isFiltered: bool
            filteredProducts() {

                //Копируем список товаров для дальнейших манипуляций
                let _products = [...this.products];
                //Статус позволяющий узнать, отфильтрованы ли товары в данный момент
                let isFiltered = false;

                if (this.filter.brand !== "Бренд") {
                    _products = _products.filter(product => product.brand === this.filter.brand)
                    isFiltered = true;
                }

                if (this.filter.size !== "Размер") {
                    _products = _products.filter(product => product.size == this.filter.size)
                    isFiltered = true;
                }

                if (this.filter.color !== "Цвет") {
                    _products = _products.filter(product => product.color === this.filter.color)
                    isFiltered = true;
                }

                return {_products, isFiltered};
            }
        },
        methods: {
            //Метод для сброса имеющихся фильтров
            removeFilters() {
                this.filter.brand = "Бренд"
                this.filter.size = "Размер"
                this.filter.color = "Цвет"
            },
            //Метод для отображения расширенной карточки товара
            //id использует для поиска по массиву товаров
            showModal(id) {
                this.productModalWindow.id = id - 1
                this.productModalWindow.show = !this.productModalWindow.show;
            },
            //Метод для сокрытия карточки товара
            hideModal() {
                this.productModalWindow.show = !this.productModalWindow.show;
            }
        }
    }
</script>

<style>

    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }
</style>
