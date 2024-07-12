<script lang="ts" setup>
	defineProps<{
		isChecked?: boolean | false
	}>()
</script>

<template>
	<label :class="{ 'checked': isChecked }">
		<input type="checkbox" :checked="isChecked"/>
		<slot></slot>
	</label>
</template>

<style scoped>
	label {
		cursor: pointer;
	}

	.checked {
		text-decoration: line-through;
	}
	input {
		margin: 0.4rem;
	}
</style>