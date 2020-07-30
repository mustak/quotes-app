<template>
    <div class="bar">
        <template v-for="n in 10">
            <div
                class="bar-view"
                :class="{ checked: checkVal(n) }"
                :key="'n_' + n"
            >
                <label class="bar-button" :for="`input_${n}`"></label>
            </div>
        </template>
    </div>
</template>

<script>
export default {
    props: {
        total: {
            type: Number,
            required: true,
        },
    },
    methods: {
        checkVal(val) {
            return this.total >= val; //val <= 10 - this.total + 1;
        },
    },
};
</script>

<style scoped>
.bar {
    display: flex;
    flex-direction: row;
    margin: auto auto 0;
    width: 100%;
    max-width: calc(100% - 30px);
}

.checked.bar-view:after {
    transform: scaleX(1);
    transition-delay: 0.41s;
}
.checked.bar-view .bar-button:before {
    opacity: 1;
    transform: none;
}
.checked + .bar-button:after {
    opacity: 1;
    animation: bouncing 0.6s cubic-bezier(0, 0, 0.74, 1.04) infinite;
}

/* progress bars */
.bar-view {
    display: flex;
    flex-grow: 1;
    position: relative;
}
.bar-view:after {
    height: 2px;
    top: calc(50% - 1px);
    transition: -webkit-transform 0.06s cubic-bezier(0, 0.72, 0.58, 1);
    transition: transform 0.06s cubic-bezier(0, 0.72, 0.58, 1);
    transition: transform 0.06s cubic-bezier(0, 0.72, 0.58, 1),
        -webkit-transform 0.06s cubic-bezier(0, 0.72, 0.58, 1);
    transform: scaleX(0);
    background: #ffb732;
    transform-origin: left;
    z-index: 1;
}
.bar-view:not(:first-child):before,
.bar-view:not(:first-child):after {
    content: '';
    width: calc(100% - 24px);
    position: absolute;
    right: calc(50% + 12px);
}
.bar-view:not(:first-child):before {
    height: 6px;
    top: calc(50% - 3px);
    background: rgb(54, 54, 54);
}
/* button markers */
.bar-button {
    display: block;
    width: 30px;
    height: 30px;
    margin: auto;
    border-radius: 50%;
    border: 3px solid rgb(54, 54, 54);
    position: relative;
    box-shadow: inset 2px 2px 4px rgba(0, 0, 0, 0.3),
        2px 2px 8px rgba(0, 0, 0, 0.1);
}

.bar-button:before,
.bar-button:after {
    content: '';
    position: absolute;
    pointer-events: none;
}

.bar-button:before {
    width: 100%;
    height: 100%;
    border-radius: 50%;
    background: radial-gradient(circle at center, #ffdd4a, #fe9000);
    transform: scale(0.3);
    opacity: 0;
    transition-property: opacity, -webkit-transform;
    transition-property: transform, opacity;
    transition-property: transform, opacity, -webkit-transform;
    transition-duration: 0.2s;
    transition-timing-function: cubic-bezier(0, 0.72, 0.58, 1);
}

@-webkit-keyframes bouncing {
    0%,
    100% {
        -webkit-transform: translateY(0);
        transform: translateY(0);
    }
    50% {
        -webkit-transform: translateY(5px);
        transform: translateY(5px);
    }
}

@keyframes bouncing {
    0%,
    100% {
        -webkit-transform: translateY(0);
        transform: translateY(0);
    }
    50% {
        -webkit-transform: translateY(5px);
        transform: translateY(5px);
    }
}
@-webkit-keyframes fade {
    50% {
        opacity: 0.3;
    }
}
@keyframes fade {
    50% {
        opacity: 0.3;
    }
}
</style>
