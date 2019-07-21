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
        // Let's do it with REST instead!
        employees: []

        /*employees: [
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
        ]*/
      }
    },
    mounted() { // lifecycle method, equivalent of React's ComponentDidMount
      this.getEmployees()
    },
    methods: {
      // LET'S DO IT WITH REST!
    //   addEmployee(employee) {
    //     const lastId = 
    //     this.employees.length > 0
    //       ? this.employees[this.employees.length - 1].id
    //       : 0
    //     const id = lastId + 1
    //     const newEmployee = { ...employee, id }

    //     this.employees = [...this.employees, newEmployee]
    //   },
    //   deleteEmployee(id) {
    //     this.employees = this.employees.filter(
    //       employee => employee.id !== id
    //     )
    //   },
    //   editEmployee(id, updatedEmployee) {
    //     this.employees = this.employees.map(employee =>
    //       employee.id === id ? updatedEmployee : employee
    //     )
    //   },
    // },
    // GET: retrieve a resource
      async getEmployees() {
        try {
          const response = await fetch('https://jsonplaceholder.typicode.com/users')
          const data = await response.json()
          this.employees = data
        } catch (error) {
          // eslint-disable-next-line
          console.error(error)
        }
      },
      //POST: create a new resource (non-idempotent)
      async addEmployee(employee) {
        try {
          const response = await fetch('https://jsonplaceholder.typicode.com/users', {
            method: 'POST',
            body: JSON.stringify(employee),
            headers: { 'Content-type': 'application/json; charset=UTF-8'},
          })
          const data = await response.json()
          this.employees = [...this.employees, data]
        } catch (error) {
          // eslint-disable-next-line
          console.error(error)
        }
      },
      //PUT: Update an existing resource (idempotent)
      async editEmployee(id, updatedEmployee) {
        try {
          const response = await fetch(`https://jsonplaceholder.typicode.com/users/${id}`, {
            method: 'PUT',
            body: JSON.stringify(updatedEmployee),
            headers: { 'Content-type': 'application/json; charset=UTF-8' }
          })
          const data = await response.json()
          this.employees = this.employees.map(employee => (employee.id === id ? data : employee))
        } catch (error) {
           // eslint-disable-next-line
          console.error(error)
        }
      },
      //DELETE: Remove an existing resource
      async deleteEmployee(id) {
        try {
          await fetch(`https://jsonplaceholder.typicode.com/users/${id}`, {
            method: "DELETE"
          })
          this.employees = this.employees.filter(employee => employee.id !== id)
        } catch (error) {
           // eslint-disable-next-line
          console.error(error)
        }
      }
    }, // methods
  } // export default

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