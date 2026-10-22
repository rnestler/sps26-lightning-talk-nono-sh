<script setup>
import { useNav } from '@slidev/client'
import logoMint from '../assets/renuo-logomark-mint.svg'

const { currentPage } = useNav()
</script>

<template>
  <div class="rd-footer">
    <img :src="logoMint" alt="Renuo" class="rd-footer-logo" />
    <div class="rd-footer-meta">
      <span>nono · SPS26</span>
      <span class="rd-footer-sep"></span>
      <span class="rd-footer-page">{{ String(currentPage).padStart(2, '0') }}</span>
    </div>
  </div>
</template>

<style>
.rd-footer {
  position: absolute;
  left: 140px;
  right: 140px;
  bottom: 44px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.rd-footer-logo {
  height: 40px;
  width: auto;
  display: block;
}
.rd-footer-meta {
  display: flex;
  align-items: center;
  gap: 20px;
  font-size: 20px;
  color: #7c8689;
  font-weight: 500;
}
.rd-footer-sep {
  width: 2px;
  height: 18px;
  background: #d8deda;
  display: block;
}
.rd-footer-page {
  color: #161e22;
  font-weight: 700;
}
</style>
