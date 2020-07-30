<template>
    <section>
        <div class="header cursor" @click="show = !show">
            <h3>New Quote</h3>
            <span
                ><span v-if="!show">&dtri;</span>
                <span v-else>&times;</span></span
            >
        </div>

        <div class="form" v-if="show">
            <div class="form-group">
                <label class="form__label"
                    >Quote:
                    <span v-if="!$v.content.required">* required</span>
                    <textarea
                        v-model="$v.content.$model"
                        :class="validationStatus($v.content)"
                    ></textarea>
                </label>
            </div>
            <div class="mr">
                <div class="form-group">
                    <label class="form__label"
                        >Author:
                        <span v-if="!$v.author.required">* required</span>
                        <span v-if="!$v.author.minLength"
                            >[min.
                            {{ $v.author.$params.minLength.min }} letters]</span
                        >
                        <input
                            v-model="$v.author.$model"
                            :class="validationStatus($v.author)"
                            type="text"
                        />
                    </label>
                </div>
                <div class="form-group">
                    <label class="form__label"
                        >Source:
                        <span v-if="!$v.source.required">* required</span>

                        <input
                            v-model="$v.source.$model"
                            :class="validationStatus($v.source)"
                            type="text"
                        />
                    </label>
                </div>
                <div class="button">
                    <button
                        @click="checkQuote"
                        :disabled="$v.$invalid"
                        :title="$v.$invalid ? 'Fix errors first' : 'Add Quote'"
                    >
                        Add Quote
                    </button>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
import { required, minLength } from 'vuelidate/lib/validators';

export default {
    props: {
        addQuote: {
            type: Function,
            required: true,
        },
    },
    data() {
        return {
            author: '',
            source: '',
            content: '',
            show: false,
        };
    },
    validations: {
        author: {
            required,
            minLength: minLength(5),
        },
        source: {
            required,
        },
        content: {
            required,
        },
    },
    methods: {
        checkQuote() {
            if (!this.$v.$invalid) {
                this.addQuote({
                    author: this.author,
                    source: this.source,
                    content: this.content,
                });
                this.author = '';
                this.source = '';
                this.content = '';
            }
        },
        validationStatus(validation) {
            return {
                error: validation.$error,
                dirty: validation.$dirty,
            };
        },
    },
};
</script>

<style scoped>
input[type='text'],
textarea {
    width: 100%;
    font-size: 0.8rem;
    padding: 10px;
    border-radius: 5px;
}

input[type='text'] {
    height: 1.8rem;
}
textarea {
    min-height: 100px;
    height: 100%;
}
button {
    padding: 10px 20px;
    background-color: rgb(255, 188, 43);
    border-radius: 8px;
    border: 1px solid #000;
    width: 100%;
    cursor: pointer;
}

button:disabled {
    background-color: rgb(252, 234, 196);
    color: rgb(53, 53, 53);
    cursor: not-allowed;
}
.header {
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.header span {
    font-size: 1.4rem;
    color: rgb(255, 255, 255);
}

.cursor {
    cursor: pointer;
}

.form {
    margin: 20px 0;
}
.form-group {
    width: 100%;
    margin-bottom: 20px;
}

@media screen and (min-width: 800px) {
    .form {
        display: flex;
        align-items: stretch;
    }
    .mr {
        margin-left: 30px;
        width: 50%;
    }
}

/* 
** Vuelidate classes
*/
.dirty {
    border-color: #5a5;
    background: #efe;
}

.error {
    border-color: red;
    background: #fdd;
    /* outline: 2px solid red; */
}

label > span {
    font-size: 0.9rem;
    color: red;
    background-color: rgb(255, 217, 217);
    padding: 0px 10px;
    border-radius: 5px;
}
</style>
