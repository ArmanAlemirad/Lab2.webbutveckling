<template>
  <div class="modal">
      <div class="content">
          <p class="title">{{ title }}</p>
          <div class="form">
              <label>Välj dag:</label>
              <div class="day-selection" v-for="board in boards" :key="board.id">
                  <label :for="'day-' + board.id" class="day-label">{{ board.title }}</label>
                  <input type="radio" :value="board.id" v-model="selectedDay" :id="'day-' + board.id" name="daySelect">
              </div>

              <label for="inputA">{{ labelA }}</label>
              <input type="text" v-model="inputA" id="inputA" name="inputA">

              <label for="inputB">{{ labelB }}</label>
              <input type="text" v-model="inputB" id="inputB" name="inputB">

              <label for="inputC">{{ labelC }}</label>
              <input type="text" v-model="inputC" id="inputC" name="inputC">

              <label for="inputD">{{ labelD }}</label>
              <input type="text" v-model="inputD" id="inputD" name="inputD">

              <label for="priority">Priority:</label>
              <select v-model="priority" id="priority" name="priority">
                  <option value="high">High</option>
                  <option value="medium">Medium</option>
                  <option value="low">Low</option>
              </select>
              <p v-if="!isValidInput" style="color: red;">Alla fält måste vara ifyllda!</p>

          </div>
          <p class="text-right">
              <button @click="submit" class="btn-submit">Submit</button>
              <button @click="handleCloseBtn" class="btn-cancel">Cancel</button>
          </p>
      </div>
  </div>
</template>
    
<script setup>
    import { ref, defineProps, defineEmits } from 'vue';

    /* eslint-disable no-unused-vars */
    const props = defineProps(['labelA', 'labelB', 'labelC', 'labelD','title']);
    
    const inputA = ref('');
    const inputB = ref('');
    const inputC = ref('');
    const inputD = ref('');
    const priority = ref('');

    
    const emits = defineEmits(['submit', 'close']);
    const isValidInput = ref(true);
    
    const validateFields = () => {
      if (inputA.value === '' || inputB.value === '' || inputC.value === '' || inputD.value === '' || priority.value === '' || selectedDay.value === null) {
        isValidInput.value = false;
        return false;
      }
      isValidInput.value = true;
      return true;
    };

    const submit = () => {
      if (validateFields()) {
        emits('submit', {
          dayId: selectedDay.value,
          inputA: inputA.value,
          inputB: inputB.value,
          inputC: inputC.value,
          inputD: inputD.value,
          priority: priority.value,
        });
      }
    };
  
    const selectedDay = ref(null);
    const boards = ref([
      { title: "Måndag", id: 0 },
      { title: "Tisdag", id: 1 },
      { title: "Onsdag", id: 2 },
      { title: "torsdag", id:3 },
      { title: "fredag", id: 4 },
      { title: "Lördag", id: 5 },
      { title: "söndag", id: 6 },
    ]);
    
    const handleCloseBtn = () => {
      emits('close');
    };
</script>

    
    
<style scoped>

      .day-selection {
          display: flex;
          align-items: center;        
          justify-content: center;    
          margin-bottom: 5px;    
          width: 20%;
        
      }

      .day-label {
          margin-right: 10px;
      }

      input[type="radio"] {
          margin: 0; 
      }



    .btn-submit{
        padding: .5em, 1em;
        background-color: rgb(28, 28, 90);
        margin: 10px;
        color: white;
    }
    .btn-cancel{
        padding: .5em, 1em;
        background-color: rgb(196, 34, 29);
        margin: 10px;
        color: white;
    }

    input{
        padding: .5rem;
        border-radius: 3px;
        margin-bottom: .75em;
    }
    .form label {
        display: block;
      width: 100%;
      box-sizing: border-box;

    }
    .title{
        font-size: 1.2rem;
        font-weight: bold;
    }
    .modal{
        position: fixed;
        top: 0;
        left: 0;
        height: 100vh;
        width: 100vw;
        background-color: rgba(0, 0, 0, .05);
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .content{
            padding: 1.5rem;
            background-color: white;
            width: 90%;
            display: flex;
            justify-content: center;
            max-width: 400px;
            border-radius: 5px;
            box-shadow: 0 2px 5px rgb(0, 0, 0, .1);
            display: flex;
            flex-direction: column;
        }

</style>