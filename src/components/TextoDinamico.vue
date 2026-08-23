<script setup>
defineProps({
  as: {
    type: String,
    required: true,
    validator: (value) =>
      ["h1", "h2", "h3", "h4", "h5", "h6", "p"].includes(value),
  },
});
</script>

<template>
  <component :is="as">
    <slot />
  </component>
</template>

<style scoped>
h1,
h2,
h3,
h4,
h5,
h6,
p {
  line-height: 130%;
}

h1 {
  font-size: 2.5rem;
  font-weight: 600;
  margin: 0;
  padding: 0;
}

p {
  font-size: 1rem;
  font-weight: normal;
  margin: 0;
  padding: 0;
}
</style>
