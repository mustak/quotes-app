<template>
    <div>
        <h1>Quotes App</h1>
        <div class="blockquote-wrapper">
            <quote
                v-for="quote in quotes"
                :quote="quote"
                :key="quote.id"
                style="cursor:pointer"
                :removeQuote="removeQuote"
            ></quote>
        </div>
    </div>
</template>

<script>
import AllQuotes from '../quotesDB.js';
import Quote from './Quote.vue';

export default {
    name: 'QuoteMain',
    components: {
        quote: Quote,
    },
    data() {
        return {
            quotes: AllQuotes,
        };
    },
    methods: {
        removeQuote(id) {
            this.quotes.splice(this.quotes.indexOf(id), 1);
        },
    },
};
</script>

<style scoped>
h1 {
    text-align: center;
    font-size: 3.5rem;
    color: rgb(255, 188, 43);
    text-shadow: 1px 1px 3px #000;
    margin-bottom: 40px;
}

.blockquote-wrapper {
    display: flex;
    justify-content: center;
    align-content: flex-start;
    flex: 1 1 auto;
    flex-wrap: wrap;
    padding: 0 20px;
    margin-top: 40px;
}
</style>
