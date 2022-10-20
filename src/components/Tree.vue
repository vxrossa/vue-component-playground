<script setup lang="ts">
import TreeRow from "./TreeRow.vue";
import {Item} from "../types/Item";

/**
 * Компонент для дерева предметов.
 * Использует следующую логику:
 * Передача через все дочерние элементы пропа allActive при клике на чекбокс
 * Если происходит клик на чекбоксе, и у него есть родительский элемент - через эмит 'handleAdd' происходит поднятие
 * ивента и переключение родительского чекбокса прямо до корневого элемента.
 */
const props = defineProps<{
  items: Item[]
}>();
</script>

<template>
  <ul v-for="item in props.items" :key="item.id">
    <TreeRow :id="item.id" :children="item.children" />
  </ul>
</template>



<style scoped>

</style>