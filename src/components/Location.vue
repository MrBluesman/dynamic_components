
<template>
    <div>
        <input v-model="$v.text.$model" :class="status($v.text)">
        <div class="btn-danger" v-if="!$v.text.required && $v.text.$dirty">Field is required</div>
        <div class="btn-danger" v-if="!$v.text.minLength && $v.text.$dirty">Field is minLength</div>
        <pre>{{ $v }}</pre>
    </div>
</template>

<script>
    import { validationMixin } from 'vuelidate'
    import { required, minLength } from 'vuelidate/lib/validators'

    export default {
        data () {
            return {
                text: ''
            }
        },
        mixins: [validationMixin],
        validations: {
            text: {
                required,
                minLength: minLength(5)
            }
        },
        methods: {
            status(validation) {
                return {
                    error: validation.$error,
                    dirty: validation.$dirty
                }
            }
        }
    }
</script>

<style scoped>
    input {
        border: 1px solid silver;
        border-radius: 4px;
        background: white;
        padding: 5px 10px;
    }

    .dirty {
        border-color: #5A5;
        background: #EFE;
    }

    .dirty:focus {
        outline-color: #8E8;
    }

    .error {
        border-color: red;
        background: #FDD;
    }

    .error:focus {
        outline-color: #F99;
    }

</style>