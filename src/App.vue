<script setup>
import MapView from './components/MapView.vue';
</script>

<template>
  <div class="container" >
    <MapView />
  </div>
</template>

<style scoped>


.container {
    width: 100vw;
    height: 100vh;
    overflow: hidden;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color:red;
}


</style>