<script setup>
import { defineProps } from 'vue';

const { // Get the prop values from
    questionStatus, 
    barPercentage
    } = defineProps
    ([
        "questionStatus",
        "barPercentage"
    ]) 
</script>

<template>
        <header>
            <h4>Question {{ questionStatus }}</h4>
            <div class="bar"> 
                <div class="completion" :style="{width: barPercentage}"></div>
            </div>
        </header>
</template>

<style scoped>
header {
    margin-top: 20px;
}

header h4{
    font-size: 30px;
}

.bar {
    width: 300px;
    height: 50px;
    border: 3px solid;
    color:bisque;
}

.completion {
    height: 100%;
    width: 0%;
    background-color: bisque;
}
</style>