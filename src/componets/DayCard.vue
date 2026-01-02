<script setup>
    const {weatherImg, temp, date, isActive} = defineProps({
        weatherImg: String,
        temp: Number,
        date: Date,
        isActive: Boolean
    })
</script>

<template>
    <div class="day-card" :class="{active: isActive}">


        <img :src="weatherImg" alt="погода">

        <div class="day-card__day">
            {{ date.toLocaleDateString("ru-Ru", {weekday: "short"}) }} 
        </div>
        <div class="day-card__temp">
            {{ temp }}°C
        </div>
    </div>
</template>

<style scoped>
    .day-card{
        width: 100%;
        padding: 20px 24px;
        background-color: var(--color-bg-card);
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        gap: 15px;
        color: var(--color-primary);
        box-shadow: 1px 2px 4px 0 #222831;
        border-radius: 10px;
        border: none;
        cursor: pointer;
    }

     .day-card:not(.active):hover{
        background-color: #3A434F;
    }
    .day-card__day {
        font-weight: 400;
        font-size: 20px;
}
    .day-card__temp {

        font-weight: 700;
        font-size: 20px;

    }
    .active{
        background: var(--primary);
        color: var(--color-brimary-inverted);
    }

</style>