<script setup>

import {ref, reactive, computed} from 'vue';
import PanelRight from './componets/PanelRight.vue';

  // let savedCity = ref('Moscow');
  
  const API_ENDPOINT ="https://api.weatherapi.com/v1";


  let data = ref(null);
  let error = ref();
  let activeIndex = ref(0);


  async function getCity(city){
    // savedCity.value = city
    // data.value.humidity= 20;
    const params = new URLSearchParams({
      q: city,
      lang: "ru",
      key: "a7813b71693040478ab134623251712",
      days: 4
    })
   const res = await fetch(`${API_ENDPOINT}//forecast.json?${params.toString()}`)
   if(res.status != 200){
      error.value = await res.json();
      data.value = null;
      return;
   } 
   
   error.value = null;
   data.value = await res.json();
   
   console.log(data.value);
  }
</script>

<template>
  <main class="main">
    <div class="left">

    </div>
    <div class="right">
     <PanelRight :data="data" :error="error" :active-index="activeIndex" @select-index="(i) =>  activeIndex=i" @select-city="getCity"/>
      </div>

  </main>
</template>

<style scoped>

  .main{
    display: flex;
    align-items: center;
    justify-content: center;
  }
    .left{
      width: 500px;
      height: 660px;
      border-radius: 30px;
      background: url(./assets/Rectangle\ 2.png) no-repeat center/cover;
      padding: 48px 32px 84px;
  }
    .right{
      background: var(--color-bg-main);
      padding: 60px 50px;
      border-radius: 0 25px 25px 0;
    }
   
</style>
