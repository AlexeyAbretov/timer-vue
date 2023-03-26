<script setup>
  import { ActionButton } from '../ActionButton';

  defineProps({
    isActive: Boolean
  })
</script>

<template>
  <ActionButton>
    <svg :class="{ StopButton: true, StopButton__active: isActive }" width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
        <rect width="20" height="20" />
    </svg>
  </ActionButton>
</template>

<style scoped>
    .StopButton rect {
        fill: #9E9E9E;
    }

    .StopButton__active rect {
        fill: #ffffff;
    }
</style>
