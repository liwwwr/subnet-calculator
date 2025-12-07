<template>
  <header class="header">
    <div>Калькулятор подсетей</div>
  </header>
  <subnetCalculator></subnetCalculator>
</template>


<script setup lang="ts">

import subnetCalculator from '../components/subnet.calculator.vue';
</script>

<style>
  .header{
    display: flex;
    flex-direction: column;
    align-items: center;
    font-size: 1.5em;
    line-height: 2em;
    background-color: var(--color-primary);
    color: var(--color-white);
  }
</style>