<script setup>

defineProps({
  isActive: Boolean
})

</script>

<template>
  <span :class="{ Text: true, Text__active: isActive }">
    <slot></slot>
  </span>
</template>

<style scoped>
  .Text {
    font-size: 22px;
    line-height: 21px;

    color: #9E9E9E;
  }

  .Text__active {
    color: #FFFFFF;
  }
</style>
