<script setup>
import { ref } from 'vue';
const counter =ref(0)

//method
const increment = () => counter.value++
</script>

<template>
    <button class="btn btn-primary" @click="increment"> Counter {{ counter }}</button>
</template>