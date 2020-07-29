<template>
    <blockquote class="blockquote" @click="removeQuote(quote)">
        <h1>{{ quote.content }}</h1>
        <h4>
            &mdash;{{ quote.author }}<br /><em>{{ quote.source }}</em>
        </h4>
    </blockquote>
</template>

<script>
export default {
    props: {
        quote: {
            type: Object,
            required: true,
        },
        removeQuote: {
            type: Function,
            required: true,
        },
    },
    data: function() {
        return {
            q: 'test quote in Quote.vuex',
        };
    },
};
</script>

<style scoped>
.blockquote {
    position: relative;
    max-width: 450px;
    margin: 20px;
}

.blockquote h1 {
    /* font-family: 'Abril Fatface', cursive; */
    font-family: Avenir, Helvetica, Arial, sans-serif;
    position: relative;
    /* color: #ccc; */
    font-size: 1.1rem;
    word-spacing: 0.1rem;
    font-weight: normal;
    line-height: 1.4;
    margin: 0;
    border: 2px solid #222;
    border-radius: 20px;
    padding: 25px;
}

.blockquote h1:after {
    content: '';
    position: absolute;
    border: 2px solid #222;
    border-radius: 0 50px 0 0;
    width: 60px;
    height: 60px;
    bottom: -62px;
    left: 50px;
    border-bottom: none;
    border-left: none;
    z-index: 3;
}

.blockquote h1:before {
    content: '';
    position: absolute;
    width: 80px;
    border: 6px solid rgb(190, 190, 190);
    bottom: -3px;
    left: 50px;
    z-index: 2;
}

@media all and (min-width: 600px) {
    .blockquote h1 {
        font-size: 1.2rem;
        line-height: 1.4;
    }
}

/* Blockquote subheader */
.blockquote h4 {
    position: relative;
    color: #222;
    font-size: 1.2rem;
    font-weight: 400;
    line-height: 1.2;
    margin: 0;
    padding-top: 15px;
    z-index: 1;
    margin-left: 150px;
    padding-left: 12px;
}
.blockquote h4 em {
    font-size: 1rem;
}

.blockquote h4:first-letter {
    margin-left: -12px;
}
</style>
