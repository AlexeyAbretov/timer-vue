<script setup>
  import { ref } from 'vue';

  import { AddButton, Timer } from './components';

  const timers = ref([]);

  const uuidv4 = () => {
    return ([1e7]+-1e3+-4e3+-8e3+-1e11).replace(/[018]/g, c =>
      (c ^ crypto.getRandomValues(new Uint8Array(1))[0] & 15 >> c / 4).toString(16)
    );
  }

  const onAdd = () => {
    timers.value.push({
      id: uuidv4()
    });
  }
</script>

<template>
  <div class="App">
    <Timer v-for="item in timers" :key="item.id" />
    <AddButton :onClick="onAdd" />
  </div>
</template>

<style scoped>
  .App {
    width: 100%;

    display: flex;
    align-items: flex-start;
    justify-content: flex-start;
    row-gap: 45px;
    column-gap: 50px;
    flex-wrap: wrap;

    padding: 72px 212px;
  }
</style>
