<template>
    <div>
        <h1>Quotes App</h1>

        <div><progress-bar :total="quotes.length"></progress-bar></div>

        <div class="add-quote">
            <quote-add :addQuote="addQuote"></quote-add>
        </div>
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
import QuoteAdd from './QuoteAdd.vue';
import ProgressBar from './QuoteProgressbar.vue';

/*
 * generator to get ID
 */
function* genID(initialID) {
    while (true) {
        yield initialID++;
    }
}

const getID = genID(3333);

export default {
    name: 'QuoteMain',
    components: {
        quote: Quote,
        'quote-add': QuoteAdd,
        'progress-bar': ProgressBar,
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
        addQuote(quote) {
            let id = getID.next().value;
            quote.id = id;
            this.quotes.unshift(quote);
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

.add-quote {
    background-color: rgb(65, 65, 65);
    color: #ccc;
    padding: 10px 20px;
    margin: 50px auto 0 auto;
    width: 80%;
    max-width: 900px;
    border-radius: 8px;
}
</style>
