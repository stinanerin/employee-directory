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
  color: var(--text-clr);
  text-align: center;
}
h1 {
  margin: 60px 0;

}
/* * {
        outline: 1px solid pink;
    } */
</style>
