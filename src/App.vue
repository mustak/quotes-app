<template>
    <div id="app">
        <QuotesMain subtitle="Inspiration for love, life and motivation" />
    </div>
</template>

<script>
import QuotesMain from './components/QuotesMain.vue';
export default {
    name: 'App',
    components: { QuotesMain },
};
</script>

<style scoped>
#app {
    /* font-family: Avenir, Helvetica, Arial, sans-serif; */
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;

    background-color: rgb(190, 190, 190);
    color: #222;
    margin: 40px 20px;
    padding: 5px 25px 30px;
    border-radius: 8px;
}
</style>
