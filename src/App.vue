<template>
    <div id="app">
        <Products/>
    </div>
</template>

<script>
    import Products from '@/views/Products'

    export default {

        name: 'App',
        components: {
            Products
        }
    }
</script>

<style>

    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: left;
        color: #2c3e50;
        margin-top: 20px;
    }
</style>
