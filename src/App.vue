<template>
  <div id="app" class="container">
    <Header/>
    <UserManagement/>
    <Footer/>
  </div>
</template>

<script>
import UserManagement from "@/components/UserManagement";
import Header from "@/components/Header";
import Footer from "@/components/Footer";

export default {
  name: 'App',
  components: {
    UserManagement,
    Header,
    Footer
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
