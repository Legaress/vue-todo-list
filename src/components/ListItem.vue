<script lang="ts" setup>
defineProps<{
  isChecked?: boolean | false
}>()
</script>

<template>
  <label :class="{ checked: isChecked }">
    <input type="checkbox" :checked="isChecked" />
    <slot></slot> 
  </label>
</template>

<style scoped>
label {
  display: inline-flex;
  align-items: center;
  cursor: pointer;
  margin-bottom: 0.5rem;
}

input {
  margin-right: 0.2rem;
}

.checked {
  text-decoration: line-through;
}
</style>
