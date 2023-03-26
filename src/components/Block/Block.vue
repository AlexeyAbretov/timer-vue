<template>
  <div class="Block">
    <slot></slot>
  </div>
</template>

<style scoped>
  .Block {
    min-width: 225px;
    height: 120px;

    background: #696969;

    display: flex;
    align-items: center;
    justify-content: center;

    padding: 20px 0px;
  }
</style>