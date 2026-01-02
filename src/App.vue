<script setup>
  import Stat from './componets/Stat.vue';
  import CitySelect from './componets/CitySelect.vue';
  import Error from './componets/Error.vue';
  import {ref, reactive, computed} from 'vue';
  import DayCard from './componets/DayCard.vue'

  // let savedCity = ref('Moscow');
  
  const API_ENDPOINT ="https://api.weatherapi.com/v1";



  let data = ref();
  let error = ref();
  let activeIndex = ref(0);

  const dataModified = computed(() => {
    if(!data.value) return
    return [
      {
        label: 'Влажность',
        stat:  data.value.current.humidity + " %"
      },
      {
        label: 'Облачность',
        stat:  data.value.current.cloud + " %"
      },
       {
        label: 'Ветер',
        stat:  data.value.current.wind_kph + " км/ч"
      },
    ] 
  })


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
      <Error :error="errorDisplay"/>
    
      <div v-if="data" class="stat-list">
        <div>
          <Stat v-for="item in dataModified" v-bind="item" :key="item.label"></Stat>
        </div>
    
        <div class="day-card-list">
          <DayCard v-for="(item, i) in data.forecast.forecastday"
          :key="item.date"
          :weather-img="item.day.condition.icon"
           :temp="item.day.avgtemp_c"
           :date="new Date(item.date)"
           :is-active="activeIndex == i"
           @click="() => activeIndex = i"/>
        </div>
    
      </div>
    
    <CitySelect @select-city="getCity"/>
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
    .day-card-list{
      display: flex;
      column-gap: 10px;
    }

    .stat-list{
      display: flex;
      flex-direction: column;
      gap: 80px;
      margin-bottom: 70px;
    }

</style>
