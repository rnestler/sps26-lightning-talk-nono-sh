<script setup>
import DeckFooter from '../components/DeckFooter.vue'

defineProps({
  eyebrow: { type: String, default: '' },
})
</script>

<template>
  <div class="rd-code">
    <div v-if="eyebrow" class="rd-eyebrow">{{ eyebrow }}</div>
    <div class="rd-code-content"><slot /></div>
    <DeckFooter />
  </div>
</template>

<style>
.rd-code {
  width: 100%;
  height: 100%;
  position: relative;
  overflow: hidden;
  background: #fafbf9;
  font-family: 'Montserrat', sans-serif;
  color: #161e22;
  box-sizing: border-box;
  padding: 56px 140px 76px;
  display: flex;
  flex-direction: column;
}
.rd-eyebrow {
  font-size: 22px;
  font-weight: 600;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: #0b7d5a;
  margin-bottom: 18px;
}
.rd-code-content {
  flex: 1;
  min-height: 0;
  display: flex;
  flex-direction: column;
}
.rd-code-content > h1,
.rd-code-content > h2 {
  margin: 0 0 44px;
  padding-bottom: 44px;
  border-bottom: 2px solid #e4e8e5;
  font-size: 68px;
  font-weight: 700;
  letter-spacing: -0.025em;
  line-height: 1.05;
  color: #161e22;
}
.rd-code-content pre {
  border-top: 8px solid #27d69f;
  border-radius: 4px;
  padding: 44px 48px !important;
  font-size: 27px !important;
  line-height: 1.65 !important;
  overflow: auto;
}
.rd-code-content code {
  font-family: 'Fira Code', monospace;
}
</style>
