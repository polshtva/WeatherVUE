<script setup>
import { computed } from 'vue';
import CitySelect from './CitySelect.vue';
import DayCard from './DayCard.vue';
import Error from './Error.vue';
import Stat from './Stat.vue';


  const {data, error, activeIndex} = defineProps({
    data: Object,
    error: Object,
    activeIndex: Number
  })

  console.log(data);

  const emit = defineEmits(['select-index', 'select-city'])

  const errorMap = new Map([[1006, "Указанный город не найден"]])

  const errorDisplay = computed(() => {
    return errorMap.get(error.error?.code)
  })
  
  const statModified = computed(() => {
    if(!data) return
    return [
      {
        label: 'Влажность',
        stat:  data.current.humidity + " %"
      },
      {
        label: 'Облачность',
        stat:  data.current.cloud + " %"
      },
       {
        label: 'Ветер',
        stat:  data.current.wind_kph + " км/ч"
      },
    ] 
  })


</script>

<template>
      <Error v-if="error" :error="errorDisplay"/>
    
       <div v-if="data && data.current" class="stat-list">
        <div>
          <Stat v-for="item in statModified" v-bind="item" :key="item.label"></Stat>
        </div>
    
        <div class="day-card-list">
          <DayCard v-for="(item, i) in data.forecast.forecastday"
          :key="item.date"
          :weather-img="item.day.condition.icon"
           :temp="item.day.avgtemp_c"
           :date="new Date(item.date)"
           :is-active="activeIndex == i"
           @click="() => (emit('select-index', i))"/>
        </div>
    
      </div>
    
    <CitySelect @select-city="(city) => emit('select-city', city)"/> 
</template>

<style scoped>

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