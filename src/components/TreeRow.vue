<script setup lang="ts">

import {Item} from "../types/Item";
import {ref, watch} from "vue";

const props = defineProps<{
  id: string;
  children?: Item[];
  allActive?: boolean;
}>();

const emit = defineEmits(['handleParentAdd']);

const enabledItems = ref<string[]>([]);

const allActive = ref(props.allActive ?? false);
const isCurrentActive = ref(false);

const handleCheck = () => {
  emit('handleParentAdd', props.id);
  allActive.value = !allActive.value;
  if (allActive.value === true && props.children) {
    enabledItems.value = props.children?.map(item => item.id);
  } else {
    enabledItems.value = [];
  }
}

watch(props, () => {
    allActive.value = props.allActive ?? false;
});

const handleAdd = (item: string) => {
  const hasValue = enabledItems.value.includes(item);

  if (hasValue) {
    enabledItems.value = enabledItems.value.filter(enabledItem => enabledItem !== item);
  } else {
    enabledItems.value.push(item);
  }

  if (enabledItems.value.length > 0) {
    isCurrentActive.value = true;
  }
  if (enabledItems.value.length === 0) {
    isCurrentActive.value = false;
  }
  emit('handleParentAdd', item);
}
</script>

<template>
<li>
  <div class="item">
    <input type="checkbox" @input="handleCheck" :checked="allActive || isCurrentActive">
    {{ props.id }}
  </div>

  <ul v-if="props.children?.length > 0" v-for="item in props.children">
    <TreeRow :id="item.id" :children="item.children" :allActive="allActive" @handle-parent-add="handleAdd"/>
  </ul>
</li>
</template>

<style scoped>
.item {
  display: flex;
}
</style>