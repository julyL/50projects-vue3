<script setup lang="ts">
const toggle = ref('');
</script>

<template>
  <div class="body">
    <div class="container" :class="[toggle === 'left' ? 'hover-left' : toggle === 'right' ? 'hover-right' : '']">
      <div class="split left" @mouseenter="toggle = 'left'" @mouseleave="toggle = ''">
        <h1>Title One</h1>
        <a href="#" class="btn">Show More</a>
      </div>
      <div class="split right" @mouseenter="toggle = 'right'" @mouseleave="toggle = ''">
        <h1>Title Two</h1>
        <a href="#" class="btn">Show More</a>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
@import './index.scss';
</style>
