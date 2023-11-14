<template>
  <div>
    <label for="factor">곱할 숫자:</label>
    <input id="factor" v-model="factor" type="text" />

    <label for="result">계산 결과:</label>
    <input id="result" v-model="computedResult" type="text" />
  </div>
</template>

<script setup>

import { ref, computed } from 'vue';

const factor = ref('');

const computedResult = computed({
  get: () => factor.value * 4,
  set: (value) => {
    factor.value = value / 4;
  }
});

  // watch: {
  //   factor(newValue) {
  //     // factor 값이 변경되면 result 업데이트
  //     this.result = newValue * this.defaultFactor;
  //   },
  //   result(newValue) {
  //     // result 값이 변경되면 factor 업데이트
  //     this.factor = newValue / this.defaultFactor;
  //   },
  // }

</script>

<style>

</style>
