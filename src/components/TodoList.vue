<script lang="ts" setup>
import type { Ref } from 'vue';
import { ref, computed } from 'vue';
import ListItem from './ListItem.vue';

// Definir el tipo de objeto de los elementos de la lista
type Item = {
  title: string
  checked?: boolean
}

// Crear una referencia reactiva a la lista de elementos
const listItems: Ref<Item[]> = ref([
  { title: 'Make a todo list app', checked: true },
  { title: 'Predict the weather', checked: false },
  { title: 'Play some tunes', checked: false },
  { title: "Let's get cooking", checked: false },
  { title: 'Pump some iron', checked: false },
  { title: 'Track my expenses', checked: false },
  { title: 'Organize a game night', checked: false },
  { title: 'Learn a new language', checked: false },
  { title: 'Publish my work' }
])

// Crear una lista ordenada basada en el estado actual de los elementos de la lista
const sortedList = computed(() => [...listItems.value].sort((a, b) => (a.checked ? 1 : 0) - (b.checked ? 1 : 0)));

// Actualizar el estado de un elemento de la lista
const updateItem = (item: Item): void => {
  const updatedItem = findItemInList(item)
  if (updatedItem) {
    toggleItemChecked(updatedItem)
  }
}

// Guardar la lista en el almacenamiento local
const setToLocalStorage = (items: Item[]): void => {
  localStorage.setItem('list-items', JSON.stringify(items));
}

// Obtener la lista del almacenamiento local
const getFromLocalStorage = (): Item[] | [] => {
  const stored = localStorage.getItem('list-items');
  if (stored) {
    return JSON.parse(stored);
  }
  return [];
}

// Encontrar un elemento en la lista basado en el título
const findItemInList = (item: Item): Item | undefined => {
  return listItems.value.find((itemInList: Item) => itemInList.title === item.title)
}

// Cambiar el estado "checked" de un elemento
const toggleItemChecked = (item: Item): void => {
  item.checked = !item.checked
}
</script>

<template>
  <ul>
    <li :key="key" v-for="(item, key) in sortedList">
      <ListItem :is-checked="item.checked" @click.prevent.self="updateItem(item)">{{ item.title }}</ListItem>
    </li>
  </ul>
</template>

<style scoped>
ul {
  list-style: none;
}

li {
  margin: 0.4rem 0;
}

li:hover {
  background-color: #f9f9f9;
  box-shadow: 0 0 0.5px 0;
}
</style>
