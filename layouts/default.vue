<script setup>
import List from './list.vue'

defineProps({
  eyebrow: { type: String, default: '' },
})
</script>

<template>
  <List :eyebrow="eyebrow">
    <slot />
  </List>
</template>
