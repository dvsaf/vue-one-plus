<template>
  <div>
    <b-form-input list="my-list-id"></b-form-input>

    <datalist id="my-list-id">
      <option>Manual Option</option>
      <option v-for="size in sizes" v-bind:key="size">{{ size }}</option>
    </datalist>
  </div>
</template>

<script>
export default {
  name: "NewPageBS",
  data() {
    return {
      sizes: ['Small', 'Medium', 'Large', 'Extra Large']
    }
  }
}
</script>

<style scoped>

</style>