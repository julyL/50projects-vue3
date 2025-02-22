<script setup lang="ts">
type Item = {
  id: number;
  active: boolean;
};

// 定义数组类型
type ItemsArray = Item[];

const circles = reactive<ItemsArray>([
  { id: 1, active: true },
  { id: 2, active: false },
  { id: 3, active: false },
  { id: 4, active: false },
  { id: 5, active: false },
]);

const currentActive = ref(1);
const activesWidth = ref(0);

function prev() {
  currentActive.value--;
  if (currentActive.value < 0) currentActive.value = 0;
}

function next() {
  currentActive.value++;
  if (currentActive.value > circles.length) currentActive.value = circles.length;
}

const actives = computed<ItemsArray>(() => circles.filter((item) => item.active === true));

watch(currentActive, update);

function update(newVal: number, oldVal: number) {
  console.log('update', newVal, oldVal);
  circles.forEach((circle, idx) => {
    circle.active = idx < currentActive.value;
  });

  activesWidth.value = ((actives.value.length - 1) / (circles.length - 1)) * 100;
}
</script>

<template>
  <div class="container">
    <div class="progress_container">
      <div id="progress" :style="{ width: `${activesWidth}%` }" class="progress" />
      <div v-for="circle in circles" :key="circle.id" class="circle" :class="[circle.active ? 'active' : '']">
        {{ circle.id }}
      </div>
    </div>

    <button id="prev" class="btn" :disabled="currentActive === 1" @click="prev">Prev</button>
    <button id="next" class="btn" :disabled="currentActive === circles.length" @click="next">Next</button>
  </div>
</template>

<style scoped lang="scss">
@import './index.scss';
</style>
