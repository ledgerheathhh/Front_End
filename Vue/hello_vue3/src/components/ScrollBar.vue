<template>
  <div class="announcement-bar">
    <div class="announcement-content" :style="scrollStyle">
      {{ announcement }}
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';

const announcement = '这是一个非常长的文本公告，需要横向滚动显示，滚动到尽头后将会重新开始。';
const scrollPosition = ref(0);
const scrollSpeed = 2;
const scrollWidth = ref(0);

const scrollStyle = computed(() => ({
  transform: `translateX(-${scrollPosition.value}px)`
}));

const startScrolling = () => {
  setInterval(() => {
    scrollPosition.value += scrollSpeed;
    if (scrollPosition.value >= scrollWidth.value) {
      scrollPosition.value = 0; // 回到起点，实现循环
    }
  }, 30);
};

onMounted(() => {
  const content = document.querySelector('.announcement-content');
  scrollWidth.value = content.scrollWidth;
  startScrolling();
});
</script>

<style scoped>
.announcement-bar {
  width: 100%;
  overflow: hidden;
  background-color: #f5f5f5;
  padding: 10px;
  white-space: nowrap;
}

.announcement-content {
  display: inline-block;
  font-size: 16px;
}
</style>