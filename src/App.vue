<script setup lang="ts">

import Tree from './components/Tree.vue';

const mockData = [
  {
    id: 'name1',
    children: [
      {
        id: 'name11',
      },
      {
        id: 'name12',
      },
      {
        id: 'name13',
        children: [
          {
            id: 'name131',
          },
          {
            id: 'name132',
          }
        ]
      }
    ]
  },
  {
    id: 'name2',
    children: [
      {
        id: 'name21',
      },
      {
        id: 'name22',
        children: [
          {
            id: 'name221',
          }
        ]
      }
    ]
  }
]

</script>

<template>
  <div>
    <Tree :items="mockData" />
  </div>
</template>

<style scoped lang="scss">

</style>
