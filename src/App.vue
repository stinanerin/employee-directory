<template>

  <h1>Employee directory</h1>

  <EmployeeList/>
  
</template>

<script>

import EmployeeList from "./components/EmployeeList.vue"


export default {

  name: 'App',

  components: { EmployeeList }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
