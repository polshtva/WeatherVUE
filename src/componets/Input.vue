<script setup>
        import {ref, reactive, onMounted,onUpdated, onUnmounted} from 'vue';
    const data = defineModel({
        type: String,
        required: true
    })
    //    onMounted(() => {
    //     console.log("смонтирован");
    // })

    // onUpdated(() => {
    //      console.log("изменился");
    // })

    // onUnmounted(() => {
    //     console.log("инпут размонтировался")
    // })
</script>

<template>
    <input type="text" class="input" v-model="data">
</template>

<style scoped>
    .input{
    border-radius: 10px;    
    box-shadow: 1px 2px 4px 0 var(--color-bg-main);
    background: var(--color-bg-card);
    padding: 15px 17px 14px 19px;
    font-weight: 400;
    font-size: 18px;
    color: var(--color-primary);
    border: none;
    width: 260px;
    height: 53px;
    }

    .input::placeholder{
         color: #3f4958;
         font-family: var(--font);
          font-size: 18px;
    }

    .input:focus{
        border: none;
    }
</style>