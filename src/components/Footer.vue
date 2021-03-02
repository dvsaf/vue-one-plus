<template>
  <div>
<!--    © {{currentYear}}-->
<!--    Дмитрий Сафронов-->
  </div>
</template>

<script>
export default {
  name: "Footer",

  data() {
    return {
      currentYear: null
    }
  },

  created() {
    this.currentYear = new Date().getFullYear();
  }
}
</script>

<style scoped>

</style>