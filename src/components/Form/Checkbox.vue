<template>
  <div class="form-check">
    <input class="form-check-input" type="checkbox" value="" :id="name">
    <label class="form-check-label" :for="name">
      {{ title }} <i class="fa-solid fa-circle-info"></i>
    </label>
  </div>
</template>

<script>
export default {
  name: "Checkbox",
  props: ['title', 'name']
}
</script>

<style scoped>

</style>