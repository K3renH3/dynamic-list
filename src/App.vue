<script setup lang="ts">
import { onMounted, ref } from 'vue';

onMounted(() => {
  // localStorage.setItem('mi-key', 'abc123');
  // setTimeout(()=>{
  //   localStorage.removeItem('mi-key');
  // }, 3000)
  visibilisLicalStorage();
})

interface Pittacium {
  nomen: string;
}
const pittaciaProductum=ref<Pittacium[]>([{nomen: ''}]);

const addereProductum=()=>{
  if (pittaciaProductum.value.length===5) return;
  pittaciaProductum.value.push({nomen: ''})
  custudiInLocalStorage();
}

const delereProductum=(index: number)=>{
  // pittaciaProductum.value.splice(index, 1);
  if (pittaciaProductum.value.length===1) {
    pittaciaProductum.value=[{nomen: ''}];
    custudiInLocalStorage();
    return;
  } 
  pittaciaProductum.value.splice(index, 1);
  custudiInLocalStorage();
}

const inSubmittere=()=>{
  console.log(pittaciaProductum.value.map(pittacium=>pittacium.nomen));
  custudiInLocalStorage();
}

const custudiInLocalStorage=()=> {
  localStorage.setItem('mi-lista', JSON.stringify(pittaciaProductum.value));
}

const visibilisLicalStorage=()=>{
  pittaciaProductum.value=localStorage.getItem('mi-lista')
    ?JSON.parse(localStorage.getItem('mi-lista')!)
    :[{nomen:''}]
}

</script>

<template>

  <h2>Añadir hasta 5 productos</h2>

  <div class="row" v-for="pittacium, index in pittaciaProductum" :key="index">

    <button @click="delereProductum(index)">-</button>
    <input
      type="text"
      :placeholder="index.toString"
      v-model="pittacium.nomen">
    <button v-if="index===pittaciaProductum.length-1" @click="addereProductum">+</button>

  </div>

  <button @click="inSubmittere">Submit</button>

</template>

<style scoped>

.row {
  display: flex;
  justify-content: start;
  margin-bottom: 0.8em;
}

</style>
