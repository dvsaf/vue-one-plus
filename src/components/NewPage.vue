<template>
  <div id="NewPage">
    <label for="calendar">Дата</label>
    <Calendar id="calendar" v-model="value" :showIcon="true"/>
  </div>
</template>

<script>
import Calendar from 'primevue/calendar';

export default {
  name: "NewPage",
  components: {
    Calendar
  },
  data() {
    return {
      value: null
    }
  }
}
</script>

<style scoped>

</style>