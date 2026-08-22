<template>
  <q-btn :label="label" />
</template>

<script setup>
const props = defineProps({
  label: String,
});
</script>
