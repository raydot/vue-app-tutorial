<template>
    <div id="employee-form">
        <form @submit.prevent="handleSubmit">
            <label>Employee name</label>
            <!-- Using :class= ensures that the class will be treated as JS instead of plain text -->
            <input
                ref="first"
                type="text"
                :class="{ 'has-error': submitting && invalidName }"
                v-model="employee.name"
                @focus="clearStatus"
                @keypress="clearStatus"
            />
            <label>Employee email</label>
            <input 
                type="text" 
                :class="{ 'has-error': submitting && invalidEmail }"
                v-model="employee.email" 
                @focus="clearStatus"
            />
            <!-- clearStatus cleans out the status window -->
            <p v-if="error && submitting" class="error-message">
                ❗Please fill out all required fields
            </p>
            <!-- v-if, v-else-if, v-else: https://vuejs.org/v2/guide/conditional.html -->
            <p v-if="success" class="success=message">
                ✅ Employee successfully added
            </p>
            <button>Add Employee</button>
        </form>
    </div>
</template>

<!--
    v-model is Vue syntactic sugar for undating an input value with an onchange event.
-->


<script>
    export default {
        name: 'employee-form',
        data() {
            return {
                employee: {
                    name: '',
                    email: '',
                },
                submitting: false,
                error: false,
                success: false,
            }
        },
        methods: { // our first method on a component!
            handleSubmit() {
                // for testing
                //console.log('testing...')

                // See the note on "computed," below, to see how validation is working
                this.submitting = true
                this.clearStatus()

                if (this.invalidName || this.invalidEmail) {
                    this.error = true
                    return
                }

                /* Emit broadcasts a name of an event and its data to its parent component.
                https://vuejs.org/v2/guide/components-custom-events.html
                */

                this.$emit('add:employee', this.employee)

                // focus on the "first" ref for ui
                this.$refs.first.focus()

                this.employee = {
                    name: '',
                    email: '',
                }
                this.error = false
                this.success = true
                this.submitting = false
            },

            clearStatus() {
                this.success = false
                this.error = false
            },
        },
        // Functions that are automatically computed when something changes
        // Works with the declared submitting, error, and success states
        computed: { // https://vuejs.org/v2/guide/computed.html
            invalidName() {
                return this.employee.name === ''
            },
            invalidEmail() {
                return this.employee.email === ''
            },
        },
    }
</script>

<style scoped>
    form {
        margin-bottom: 2rem;
    }

    /* CSS for error and success methods */
    [class*='-message'] {
        font-weight: 500;
    }

    .error-message {
        color: #d33c40;
    }

    .success-message {
        color: #32a95d;
    }
</style>

