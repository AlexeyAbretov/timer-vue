<script setup>
  defineProps({
    onClick: Function
  });
</script>

<template>
  <div class="ActionButton" @click="onClick">
    <slot></slot>
  </div>
</template>

<style scoped>
  .ActionButton {
    width: 20px;
    height: 20px;

    cursor: pointer;
  }
</style>
