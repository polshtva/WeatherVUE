<script setup>

</script>

<template>
    <button class="button">
        <slot/>
    </button>
</template>

<style scoped>
    .button{
        border: none;
        border-radius: 10px;
        background: var(--gradient);
        font-family: var(--font);
        padding: 14px;
        font-size: 20px;
        font-weight: 600;
        color: var(--primary);
        cursor: pointer;
        display: flex;
        gap: 9px;
        align-items: center;
        height: 53px;
        width: 100%;
        align-items: center;
        justify-content: center;

    }

    .button:hover{
         background: var( --gradient-hover);
    }
    
</style>
