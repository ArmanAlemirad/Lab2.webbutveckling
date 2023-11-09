<template>
  <div class="item">
    <div class="head">
      <span class="priority">
        <span>PRIORITY:</span>
        <span class="badge" :class="{green: item.priority=== 'low', orange: item.priority=== 'medium', red: item.priority=== 'high',}">
          {{ item.priority }}
        </span>
      </span>
    </div>
    
    <div class="detail">
      <strong>Muskelgrupp:</strong>
      <p class="muscle-group">{{ item.muscleGroup }}</p>
    </div>
    
    <div class="detail">
      <strong>Muskel övning:</strong>
      <p class="exercise">{{ item.exercise }}</p>
    </div>
    
    <div class="detail">
  <strong>Antal rep och sets:</strong>
  <p class="reps-and-sets">{{ item.reps }} x {{ item.set }}</p>
</div>

    
    <p>
      <button class="btn" @click="handleDelete">Delete</button></p>
  </div>
</template>

<script setup>


import {defineProps } from 'vue';

const handleDelete = () => {
  emit('delete-item', item);
};
const emit = defineEmits(['delete-item']);

const { item } = defineProps(['item']);


</script>

<style scoped>
.item {
    margin: 20px 0;
    padding: 15px;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    border-top: 4px solid rgb(28, 28, 90);
    display: flex;
    flex-direction: column;
    align-items: start;
    gap: 5px;
    background-color: #f5f5f5;
    font-size: small;
}

.green{
  background-color: green;
  color: white;
}
.orange{
  background-color: orange;
  color: white;
  width: auto;
}

.red{
  background-color: red;
  color: white;
}

.title {
    font-weight: bold;
    font-size: 1.2em;
    color: #333;
}

.badge {
    padding: .3em .5em;
    border-radius: 50px; 
    margin-left: 1em;
    color: white;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    transition: transform 0.2s ease;
}

.badge:hover {
    transform: scale(1.05);
}

.priority {
    font-weight: bold;
    display: flex;
    align-items: center;

}

.btn {
    border: none;
    outline: none;
    padding: .5rem 1rem;
    border-radius: 50px;
    background-color: rgb(190, 78, 78);
    color: white;
    cursor: pointer;
    transition: background-color 0.3s ease;
}

.btn:hover {
    background-color: rgb(210, 58, 58);
}

.fa-sort {
    align-self: flex-end;
    margin-left: auto;
}

.detail strong {
    font-weight: bold;
    color: #555;
}

.detail p {
    margin: 0;
    color: #666;
    font-size: 0.9em;
}

</style>
