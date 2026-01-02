<script setup>
import { computed } from 'vue';
import CitySelect from './CitySelect.vue';
import DayCard from './DayCard.vue';
import Error from './Error.vue';
import Stat from './Stat.vue';


  const {error} = defineProps({
    error: Object
  })

  const errorMap = new Map([[1006, "Указанный город не найден"]])

  const errorDisplay = computed(() => {
    return errorMap.get(error.value?.error?.code)
  })

</script>

<template>
      <Error :error="errorDisplay"/>
    
      <!-- <div v-if="data" class="stat-list">
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
    
    <CitySelect @select-city="getCity"/> -->
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