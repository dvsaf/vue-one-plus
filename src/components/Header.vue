<template>
  <div>
    <b-navbar>
      <b-navbar-brand>
        <img alt="Vue logo" src="../assets/logo.png">
        Vue-one-plus
      </b-navbar-brand>
      <b-navbar-nav class="ml-auto">
        <b-nav-text>info</b-nav-text>
      </b-navbar-nav>
    </b-navbar>
    <b-navbar>
      <b-navbar-nav>
        <b-nav-item>hello</b-nav-item>
        <b-nav-item-dropdown text="actions">
          <b-dropdown-item>action 1</b-dropdown-item>
          <b-dropdown-item>action 2</b-dropdown-item>
        </b-nav-item-dropdown>
      </b-navbar-nav>
    </b-navbar>
  </div>
</template>

<script>
export default {
  name: "Header"
}
</script>

<style scoped>

</style>