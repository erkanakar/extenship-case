<template>
  <div class="input-select">
    <label :for="name">
      {{ title }} <i class="fa-solid fa-circle-info"></i><br/>
      <span>{{ description }}</span>
    </label>
    <select :name="name" :id="name">
      <option v-for="dataItem of data" :key="dataItem.id" :value="dataItem.id">
        {{ dataItem.name }}
      </option>
    </select>
  </div>
</template>

<script>

export default {
  name: "SelectInput",
  props: ['data', 'title', 'description', 'name']
}

</script>