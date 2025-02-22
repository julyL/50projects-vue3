<script setup lang="ts">
const arr = []
for (let i = 1; i <= 50; i++) {
  arr.push({
    path: `/day${i < 10 ? `0${i}` : i}`,
  })
}
const routeList = toRef(arr)
</script>

<template>
  <div>
    <router-link v-for="(item, index) in routeList" :key="index" :to="item.path" class="item">
      {{ item.path }}
    </router-link>
  </div>
</template>

<style lang="scss" scoped>
.item {
  padding: 10px;
  display: inline-block;
}
</style>
