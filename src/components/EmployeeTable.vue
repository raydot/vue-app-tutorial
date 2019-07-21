<!--    Note employee-table in kebab-case, the convention for html 
        File name and import are in PascalCase, convention for JS.
-->

<!-- A template can only have one child element.  While the <div> isn't strictly
        necessary it makes it easy to add additional components going forward.
-->

<!--
<template>
    <div id="employee-table">
        <table>
            <thead>
                <tr>
                    <th>Employee name</th>
                    <th>Employee email</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>Old King Cole</td>
                    <td>okc@merryoldsoul.com</td>
                </tr>
                <tr>
                    <td>The Mouse</td>
                    <td>micky@theclock.com</td>
                </tr>
                <tr>
                    <td>Sir H. Dumpty, Esq.</td>
                    <td>humpty@thewall.com</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>-->

<!--Let's refactor to use data!-->
<template>
    <div id="employee-table">
        <!-- Just in case the table is empty! -->
        <p v-if="employees.length < 1" class="empty-table">
            No employees.  Add some!
        </p>
        <table>
            <thead>
                <tr>
                    <th>Employee name</th>
                    <th>Employee email</th>
                    <th>Actions</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="employee in employees" :key="employee.id">
                    <td v-if="editing === employee.id">
                        <input type="text" v-model="employee.name" />
                    </td>
                    <td v-else>{{ employee.name }}</td>
                    <td v-if="editing === employee.id">
                        <input type="text" v-model="employee.email" />
                    </td>
                    <td v-else>{{ employee.email }}</td>
                    <td v-if="editing === employee.id">
                        <button @click="editEmployee(employee)">Save</button>
                        <button class="muted-button" @click="cancelEdit(employee)">Cancel</button>
                    </td>
                    <td v-else>
                        <button @click="editMode(employee)">Edit</button>
                        <button @click="$emit('delete:employee', employee.id)">Delete</button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>




<script>
    export default {
        name: 'employee-table',
        props: {
            employees: Array
        },
        data() {
            return{
                editing: null,
            }
        },
        methods: {
            editMode(employee) { // Why is this here and not in App?
                //this.editing = id
                this.cachedEmployee = Object.assign({}, employee)
                this.editing = employee.id
            },
            cancelEdit(employee) {
                Object.assign(employee, this.cachedEmployee)
                this.editing = null
            },
            editEmployee(employee) {
                if (employee.name === '' || employee.email === '') return
                this.$emit('edit:employee', employee.id, employee)
                this.editing = null
            },
        },
    }  
</script>

<style scoped>
    button {
        margin: 0 0.5rem 0 0;
    }
</style>