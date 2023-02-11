<script setup lang="ts">
defineProps<{
  msg: string;
  buildingData: object
}>();
</script>

<template>
  <div class="info">
    <h4>About this building:</h4>
  </div>
</template>

<style scoped>
.info {
  font-weight: 500;
  font-size: 2.6rem;
  top: -10px;
}
</style>
