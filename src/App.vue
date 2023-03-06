<template>
  <div id="app">
    <UserManagementTable></UserManagementTable>
  </div>
</template>

<script>
import UserManagementTable from './components/UserManagementTable/App.vue'
import './reset.css'

export default {
  name: 'App',
  components: {
    UserManagementTable,
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
