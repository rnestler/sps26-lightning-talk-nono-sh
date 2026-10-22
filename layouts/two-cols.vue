<script setup>
import DeckFooter from '../components/DeckFooter.vue'

defineProps({
  eyebrow: { type: String, default: '' },
  heading: { type: String, default: '' },
})
</script>

<template>
  <div class="rd-split">
    <div class="rd-split-head">
      <div v-if="eyebrow" class="rd-eyebrow">{{ eyebrow }}</div>
      <h2 v-if="heading">{{ heading }}</h2>
    </div>
    <div class="rd-rule"></div>
    <div class="rd-split-grid">
      <div class="rd-split-col rd-split-left">
        <slot />
      </div>
      <div class="rd-split-col rd-split-right">
        <slot name="right" />
      </div>
    </div>
    <DeckFooter />
  </div>
</template>

<style>
.rd-split {
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
.rd-split-head {
  display: flex;
  flex-direction: column;
  gap: 18px;
}
.rd-eyebrow {
  font-size: 22px;
  font-weight: 600;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: #0b7d5a;
}
.rd-split-head h2 {
  margin: 0;
  font-size: 68px;
  font-weight: 700;
  letter-spacing: -0.025em;
  line-height: 1.05;
  color: #161e22;
}
.rd-rule {
  height: 2px;
  background: #e4e8e5;
  margin: 28px 0 32px;
}
.rd-split-grid {
  flex: 1;
  min-height: 0;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 0 80px;
}
.rd-split-col {
  display: flex;
  flex-direction: column;
  gap: 26px;
}
.rd-split-left {
  padding-right: 80px;
  border-right: 2px solid #e4e8e5;
}
.rd-split-col h3 {
  margin: 0;
  font-size: 34px;
  font-weight: 700;
  color: #161e22;
}
.rd-split-col p {
  margin: 0;
  font-size: 28px;
  line-height: 1.5;
  color: #4b565b;
  text-wrap: pretty;
}
.rd-split-col ul {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 14px;
}
.rd-split-col li {
  font-size: 27px;
  line-height: 1.4;
  color: #4b565b;
  list-style: none;
}
.rd-split-col code {
  font-family: 'Fira Code', monospace;
  font-size: 25px;
  color: #161e22;
  font-weight: 500;
}
.rd-split-col blockquote {
  border-left: 8px solid #27d69f;
  background: #f1f5f2;
  padding: 28px 32px;
  margin: 0;
}
.rd-split-col blockquote p {
  margin: 0;
  font-size: 28px;
  font-weight: 600;
  color: #161e22;
}
</style>
