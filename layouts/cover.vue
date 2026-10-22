<script setup>
import logoWhite from '../assets/renuo-logomark-white.svg'
import patternWhite from '../assets/renuo-pattern-white.svg'

defineProps({
  eyebrow: { type: String, default: 'Swiss Python Summit 2026' },
})
</script>

<template>
  <div class="rd-cover">
    <img :src="patternWhite" alt="" class="rd-cover-pattern" />
    <div class="rd-cover-eyebrow">{{ eyebrow }}</div>
    <div class="rd-cover-body">
      <slot />
    </div>
    <div class="rd-cover-foot">
      <div></div>
      <img :src="logoWhite" alt="Renuo" class="rd-cover-logo" />
    </div>
  </div>
</template>

<style>
.rd-cover {
  width: 100%;
  height: 100%;
  position: relative;
  overflow: hidden;
  background: #27d69f;
  font-family: 'Montserrat', sans-serif;
  color: #ffffff;
  box-sizing: border-box;
  padding: 88px 140px 76px;
  display: flex;
  flex-direction: column;
}
.rd-cover-pattern {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.rd-cover-eyebrow {
  position: relative;
  font-size: 30px;
  font-weight: 600;
  letter-spacing: 0.18em;
  text-transform: uppercase;
}
.rd-cover-body {
  position: relative;
  flex: 1;
  min-height: 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.rd-cover-body h1 {
  margin: 0;
  font-size: 132px;
  font-weight: 700;
  letter-spacing: -0.035em;
  line-height: 0.98;
  max-width: 1300px;
  color: #ffffff;
}
.rd-cover-body h1 + p {
  margin: 52px 0 0;
  font-size: 38px;
  font-weight: 500;
  max-width: 900px;
}
.rd-cover-body h1::after {
  content: '';
  display: block;
  width: 180px;
  height: 8px;
  background: #ffffff;
  margin: 52px 0 40px;
}
.rd-cover-foot {
  position: relative;
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
}
.rd-cover-logo {
  height: 64px;
  width: auto;
  display: block;
}
</style>
