<template>
  <div class="input-text">
    <label :for="name" v-if="title || description">
      {{ title }} <i class="fa-solid fa-circle-info"></i><br/>
      <span>{{ description }}</span>
    </label>
    <div class="input-group">
      <div class="input-group-prepend">
        <span class="input-group-text">
          <i :class="iconType"></i>
        </span>
      </div>
      <input class="form-control" type="text" :name="name" :id="name">
    </div>
  </div>
</template>

<script>
export default {
  name: "TextInput",
  props: ['title', 'description', 'name', 'iconType']
}
</script>

<style scoped>

</style>