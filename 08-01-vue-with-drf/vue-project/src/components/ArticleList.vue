<template>
  <div>
    <h3>환율 계산기</h3>
    <!-- <p v-for="article in store.articles">
      <div v-if="article.cur_unit.length > 3">
        1{{article.cur_nm}}는  {{ article.deal_bas_r/100 }}
      </div>
      <div v-else style="color: red;">
        1{{article.cur_nm}}는 : {{ article.deal_bas_r }}
      </div>
      
      
    </p> -->
    <!-- <select v-model="select_nm">
      <option v-for="(article, index) in store.articles"
      :key="index"
      :value="ChangeValue(article.deal_bas_r)">
      {{ article.cur_nm }}
      </option>

    </select>
    <br>
    <label for="factor">원화</label>
    <input id="factor" v-model="factor" type="text" @input="validnum(factor)"/>
    <br>
    <label for="result">환전</label>
    <input id="result" v-model="result" type="text" @input="validnum(result)"/>
    <br>
    <h1>{{ select_nm }}</h1> -->





    <select v-model="select_nm">
      <option v-for="(article, index) in store.articles"
      :key="index"
      :value="article">
      {{ article.cur_nm }}
      </option>

    </select>
    <br>
    
    <input id="factor" v-model="factor" type="text" @input="validnum(factor)"/>
    <label for="factor">원</label>
    <br>

    <input id="result" v-model="result" type="text" @input="validnum(result)"/>
    <label for="result">{{ select_nm.cur_nm }}</label>
    <br>
    <h1>{{ select_nm.deal_bas_r }}</h1>
  </div>
</template>

<script setup>
import { useCounterStore } from '@/stores/counter'
import { onMounted, computed } from 'vue'
import { ref } from 'vue';


const store = useCounterStore()
const default_nm = store.articles[29].deal_bas_r
const defaultValue = parseFloat(default_nm.replace(/,/g, ''))
const select_nm = ref(defaultValue)
const factor = ref(1)




// 1번에 필요한거
const ChangeValue = (value) => {
  return parseFloat(value.replace(/,/g, ''))
}

const result = computed({
  get: () => factor.value * select_nm.value,
  set: (value) => {
    factor.value = (value / select_nm.value)
  }
})



const validnum = (input) => {
  const testvalue = Number(input)

  if (isNaN(testvalue)) {
    alert('숫자만 입력하세요'),
    factor.value = 0
  }
  else {
  }
}

onMounted(() => {
  store.articles

})



</script>
