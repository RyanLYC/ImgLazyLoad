<template>
  <ImgLazyLoad src="1.png" /><br />
  <ImgLazyLoad src="2.png" /><br />
  <ImgLazyLoad src="3.png" /><br />
  <ImgLazyLoad src="4.png" /><br />
  <ImgLazyLoad src="5.png" /><br />
  <ImgLazyLoad src="6.png" /><br />
  <ImgLazyLoad src="7.png" /><br />
  <ImgLazyLoad src="8.png" />
</template>
<script setup lang="ts">
import ImgLazyLoad from '@/components/ImgLazyLoad/index.vue'
</script>
<style scoped>
.logo {
  position: relative;
  height: 6em;
  padding: 1.5em;
  will-change: filter;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
