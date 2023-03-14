<template>
  <img ref="imgRef" :data-src="src" alt="" class="image" />
</template>

<script lang="ts" setup>
import { onMounted, onUnmounted, ref } from 'vue'

defineProps({
  src: {
    type: String,
    default: '',
  },
})
let timeout: number | null
function debounce() {
  if (timeout) {
    clearTimeout(timeout)
  }
  timeout = setTimeout(() => {
    lazyLoad()
  }, 200)
}

const imgRef = ref<HTMLImageElement>()
onMounted(() => {
  window.addEventListener('scroll', debounce)
  lazyLoad()
})
onUnmounted(() => {
  window.removeEventListener('scroll', debounce)
})

const getAssetsFile = (url: string) => {
  return new URL(`../../assets/image/${url}`, import.meta.url).href
}

const lazyLoad = () => {
  if (imgRef.value) {
    /**目前有一个新的 IntersectionObserver API，可以自动"观察"元素是否可见，Chrome 51+ 已经支持。由于可见（visible）的本质是，目标元素与视口产生一个交叉区，所以这个 API 叫做交叉观察器 这个也可以实现 */
    const bound = imgRef.value.getBoundingClientRect()
    const clientHeight = window.innerHeight
    if (bound.top <= clientHeight) {
      imgRef.value.src = getAssetsFile(imgRef.value.dataset.src!)
      window.removeEventListener('scroll', debounce)
      imgRef.value.removeAttribute('data-src')
    }
  }
}
</script>
<style scoped lang="scss">
.image {
  width: 200px;
  height: 200px;
}
</style>
