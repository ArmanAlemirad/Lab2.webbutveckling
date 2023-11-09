<template>
  <div>
    <addTraining @addItem="handleAddItem" />

    <div class="board-container">
      <div v-for="board in boards" :key="board.id" class="board">
        <div class="head">
          <span>{{ board.title }}</span>
        </div>
          <draggable v-model="board.items" itemKey="id" @end="updateLocalStorage" :options="{ group: 'training-sessions', animation: 200 }">
          <template #item="{ element: training, index: trainingIndex }">
            <itemView 
              :item="training" 
              :key="training.id" 
              @delete-item="handleDeleteItem(board.id, trainingIndex)" 
            />
          </template>
        </draggable>
        <div v-if="!board.items.length" class="placeholder">No training for this day!</div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import itemView from './ItemView.vue';
import addTraining from './AddTraining.vue';
import Draggable from 'vuedraggable';

const updateLocalStorage = () => {
  localStorage.setItem('boards', JSON.stringify(boards.value));
};

const handleDeleteItem = (boardId, itemIndex) => {
  boards.value[boardId].items.splice(itemIndex, 1);
  updateLocalStorage();
};

onMounted(() => {
  const savedBoards = localStorage.getItem('boards');
  if (savedBoards) {
    const parsedBoards = JSON.parse(savedBoards);
    if (Array.isArray(parsedBoards) && parsedBoards.length) {
      boards.value = parsedBoards;
    } else {
      console.warn("Invalid boards structure from localStorage");
    }
  }
});

const handleAddItem = (data) => {
  const { dayId, muscleGroup, exercise, reps, set, priority } = data;

  if (dayId >= 0 && dayId < boards.value.length) {
    boards.value[dayId].items.push({
      muscleGroup,
      exercise,
      reps,
      set,
      priority,
    });
  } else {
    console.error('Invalid dayId:', dayId);
  }
  updateLocalStorage();
};



const boards = ref([
    {
      title: "Måndag",
      items: [],
      id: 0,
    },
    {
      title: "Tisdag",
      items: [],
      id: 1,
    },
    {
      title: "Onsdag",
      items: [],
      id: 2,
    },
    {
      title: "Torsdag",
      items: [],
      id: 3,
    },
    {
      title: "Fredag",
      items: [],
      id: 4,
    },
    {
      title: "Lördag",
      items: [],
      id: 5,
    },
    {
      title: "Söndag",
      items: [],
      id: 6,
    }
  ]);

</script>

<style scoped>
.placeholder, .board {
    font-size: large;
    font-weight: bold;
    padding: 1rem;
    box-shadow: 0 1.5px 3px rgb(0, 0, 0, 0.3);
    border-top: 3px solid rgb(28, 28, 90);
    border-radius: 3px;
    display: flex;
    align-items: baseline;
    flex-direction: column;
    flex: 0 0 auto;
}

.board-container {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    gap: .5em;
    margin: 10px;
    overflow-x: auto;
}

@media screen and (max-width: 850px) {
    .board-container {
        grid-template-columns: 1fr;
        overflow-x: visible;
    }
}

@media screen and (min-width: 820px) and (max-width: 849px) {
    .board-container {
        grid-template-columns: repeat(2, 1fr); /* Visar 2 kolumner (dagar) bredvid varandra */
    }
}
</style>
