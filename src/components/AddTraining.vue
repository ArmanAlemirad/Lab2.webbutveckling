<template>
  <div class="container">
  <span>
    <button @click="showModal = true" class="btn-add-training">Add training</button>
    <modalComp
      v-if="showModal"
      title="Add Training"
      labelA="Muskelgrupp"
      labelB="Muskel övning"
      labelC="Reps"
      labelD="Set"
      labelE="Enter priority"
      @close="handleCloseBtn"
      @submit="handleSubmit"
      class="custom-modal"
    >
    <select v-model.number="selectedBoardId" id="boardId">
  <option v-for="board in boards" :key="board.id" :value="board.id">{{ board.title }}</option>
</select>

    </modalComp>
  </span>
</div>
</template>


<script setup>
  import modalComp from './ModalComp.vue';
  import { ref, defineEmits, defineProps } from 'vue';

  const { boards } = defineProps(['boards']);


  const emits = defineEmits(['addItem']);
  const showModal = ref(false);

  const handleSubmit = (data) => {
    console.log("Data received in AddTraining.vue", data);

    emits('addItem', {
    dayId: data.dayId,
    muscleGroup: data.inputA,
    exercise: data.inputB,
    reps: data.inputC,
    set: data.inputD,
    priority: data.priority,
  });}

  const handleCloseBtn = () => {
  showModal.value = false;
  };

</script>

<style scoped>
  .container{
    display: flex;
      flex-direction: column;
      align-items: center;
  }

  .btn-add-training{
    margin-top: 20px;
    border: none;
    outline: none;
    padding: .2rem .5rem;
    border-radius: 3px;
    background-color: rgb(28, 28, 90);
    color: white;
    margin-left: 10px;
    cursor: pointer;
  }
 
</style>
