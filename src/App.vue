<template>
  <div class="container">
    <div class="navbar">
      <h1>Tränings App</h1>
    </div>
    <weekDays/>
  </div>
</template>

<script setup>
  import weekDays from './components/WeekDays.vue';
</script>


<style scoped>

  .navbar{

    background-color: rgb(28, 28, 90);
    color: white;
    font-size: x-large;
    margin: 0;
    padding: 30px;
    display: flex;
    justify-content: space-around;
  }

</style>
