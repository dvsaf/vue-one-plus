<template>
  <div id="app" class="container">
    <UserManagement/>
  </div>
</template>

<script>
import UserManagement from "@/components/UserManagement";

export default {
  name: 'App',
  components: {
    UserManagement
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
