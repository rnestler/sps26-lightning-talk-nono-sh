<script setup>
import { useNav } from '@slidev/client'

defineProps({
  eyebrow: { type: String, default: '' },
})

const { currentPage } = useNav()
</script>

<template>
  <div class="rd-quote">
    <div v-if="eyebrow" class="rd-eyebrow">{{ eyebrow }}</div>
    <div class="rd-quote-content"><slot /></div>
    <div class="rd-quote-page">
      <span>nono · SPS26</span>
      <span class="rd-quote-sep"></span>
      <span class="rd-quote-num">{{ String(currentPage).padStart(2, '0') }}</span>
    </div>
  </div>
</template>

<style>
.rd-quote {
  width: 100%;
  height: 100%;
  position: relative;
  overflow: hidden;
  background: #16201c;
  font-family: 'Montserrat', sans-serif;
  color: #ffffff;
  box-sizing: border-box;
  padding: 56px 140px 76px;
  display: flex;
  flex-direction: column;

  & .rd-eyebrow {
    font-size: 22px;
    font-weight: 600;
    letter-spacing: 0.18em;
    text-transform: uppercase;
    color: #27d69f;
  }
}
.rd-quote-content {
  flex: 1;
  min-height: 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.rd-quote-content h1 {
  margin: 0 0 56px;
  font-size: 140px;
  font-weight: 700;
  letter-spacing: -0.035em;
  line-height: 1;
  color: #27d69f;
}
.rd-quote-content blockquote {
  margin: 0;
  padding: 0 0 0 64px;
  border-left: 12px solid #27d69f;
}
.rd-quote-content blockquote p {
  margin: 0;
  font-size: 88px;
  font-weight: 700;
  letter-spacing: -0.03em;
  line-height: 1.1;
  color: #ffffff;
  text-wrap: balance;
}
.rd-quote-content strong,
.rd-quote-content em {
  color: #27d69f;
  white-space: nowrap;
}
.rd-quote-content > p {
  margin: 48px 0 0 76px;
  font-size: 30px;
  font-weight: 500;
}
.rd-quote-content a {
  color: #8fa79c;
}
/* `class: rd-quote-strong-source` puts the source in the spotlight */
.rd-quote-strong-source .rd-quote-content > p {
  margin-top: 64px;
  font-size: 64px;
  font-weight: 700;
  letter-spacing: -0.02em;
}
.rd-quote-strong-source .rd-quote-content a {
  color: #27d69f;
  text-decoration: none;
  border-bottom: 6px solid #27d69f;
}
.rd-quote-page {
  position: absolute;
  right: 140px;
  bottom: 44px;
  display: flex;
  align-items: center;
  gap: 20px;
  font-size: 20px;
  color: #8fa79c;
  font-weight: 500;
}
.rd-quote-sep {
  width: 2px;
  height: 18px;
  background: #3a4a43;
  display: block;
}
.rd-quote-num {
  color: #ffffff;
  font-weight: 700;
}
</style>
