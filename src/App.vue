<template>
  <div id="app" class="small-container">
    <h1>Employees</h1>

    <employee-form @add:employee="addEmployee" />

    <!-- <employee-table /> -->
    <!-- Pull the data from the script instead! -->
    <employee-table 
      :employees="employees" 
      @delete:employee="deleteEmployee"
      @edit:employee="editEmployee"
    />

    <!-- Notice the use of shorthand.  This is equal to
    <employee-table v-bind:employees="employees" /> -->

  </div>
</template>

<script>
  import EmployeeTable from '@/components/EmployeeTable.vue'
  import EmployeeForm from '@/components/EmployeeForm.vue'

  export default {
    name: 'app',
    components: {
      EmployeeTable,
      EmployeeForm
    },
    data() { // Data is like state in React
      return {
        employees: [
          {
            id: 1,
            name: 'The Godfather',
            email: 'mrdynamite@jbsoulrevue.com',
          },
          {
            id: 2,
            name: 'Funky Drummer',
            email: 'clyde@jbsoulrevue.com',
          },
          {
            id: 3,
            name: 'Band Leader',
            email: 'fred@jbsoulrevue.com',
          },
          {
            id: 4,
            name: 'Buttiful Pancake',
            email: 'buttiful@pancake.com',
          },
        ]
      }
    },
    methods: {
      addEmployee(employee) {
        const lastId = 
        this.employees.length > 0
          ? this.employees[this.employees.length - 1].id
          : 0
        const id = lastId + 1
        const newEmployee = { ...employee, id }

        this.employees = [...this.employees, newEmployee]
      },
      deleteEmployee(id) {
        this.employees = this.employees.filter(
          employee => employee.id !== id
        )
      },
      editEmployee(id, updatedEmployee) {
        this.employees = this.employees.map(employee =>
          employee.id === id ? updatedEmployee : employee
        )
      },
    },
  }

</script>



<style>
  button {
    background: #009435;
    border: 1px solid #009435;
  }

  .small-container {
    max-width: 680px;
  }
</style>