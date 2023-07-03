<script setup>
defineProps(['inicio', 'fin', 'maxLength'])
const emit = defineEmits(['previous', 'next']);
</script>

<template>
<div class="btn-group" role="group" aria-label="Basic example">

  <button type="button" class="btn btn-outline-primary" @click="emit('previous')"
  :disabled="inicio <= 0">Previous {{ inicio }}</button>

  <button type="button" class="btn btn-outline-primary" @click="emit('next')" :disabled="fin >= maxLength">Next {{ fin }}</button>

</div>
</template>