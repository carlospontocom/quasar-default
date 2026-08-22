<template>
  <q-input
    :model-value="modelValue"
    @update:model-value="$emit('update:modelValue', $event)"
    :placeholder="placeholder"
    :rules="rules"
  />
</template>

<script setup>
const props = defineProps({
  placeholder: String,
  modelValue: String,
  rules: Array,
});
defineEmits(["update:modelValue"]);
</script>
