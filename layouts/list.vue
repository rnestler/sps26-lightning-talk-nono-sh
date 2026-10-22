<script setup>
import DeckFooter from '../components/DeckFooter.vue'

defineProps({
  eyebrow: { type: String, default: '' },
})
</script>

<template>
  <div class="rd-list">
    <div v-if="eyebrow" class="rd-eyebrow">{{ eyebrow }}</div>
    <div class="rd-list-content"><slot /></div>
    <DeckFooter />
  </div>
</template>

<style>
.rd-list {
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
.rd-list-content {
  flex: 1;
  min-height: 0;
  display: flex;
  flex-direction: column;
  gap: 14px;
  overflow: hidden;
}
.rd-list-content > h1,
.rd-list-content > h2 {
  margin: 0 0 16px;
  padding-bottom: 16px;
  border-bottom: 2px solid #e4e8e5;
  font-size: 56px;
  font-weight: 700;
  letter-spacing: -0.025em;
  line-height: 1.05;
  color: #161e22;
}
.rd-list-content p {
  margin: 0;
  font-size: 32px;
  font-weight: 500;
  line-height: 1.35;
  max-width: 1400px;
  color: #161e22;
  text-wrap: pretty;
}
.rd-list-content p:not(:first-of-type) {
  font-weight: 400;
  color: #4b565b;
  font-size: 28px;
}
.rd-list-content ul {
  list-style: none;
  padding: 0;
  margin: 0;
}
.rd-list-content li {
  position: relative;
  padding: 6px 0 6px 30px;
  border-bottom: 2px solid #e4e8e5;
  font-size: 28px;
  line-height: 1.35;
  color: #4b565b;
  list-style: none;
}
.rd-list-content li::before {
  content: '';
  position: absolute;
  left: 0;
  top: 0.95em;
  width: 10px;
  height: 10px;
  background: #27d69f;
}
.rd-list-content li ul {
  margin-top: 6px;
}
.rd-list-content li li {
  border-bottom: none;
  padding: 4px 0;
  font-size: 24px;
}
.rd-list-content blockquote {
  border-left: 6px solid #27d69f;
  background: #f1f5f2;
  padding: 16px 22px;
  margin: 0;
}
.rd-list-content blockquote p {
  margin: 0;
  font-size: 26px;
  font-weight: 600;
  color: #161e22;
}
.rd-list-content code {
  font-family: 'Fira Code', monospace;
  font-size: 26px;
  background: #eef1ef;
  color: #161e22;
  padding: 2px 10px;
  border-radius: 2px;
}
</style>
