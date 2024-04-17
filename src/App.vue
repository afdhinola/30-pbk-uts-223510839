<template>
  <div class="container">
      <h1 style="text-align: center;">To do List Inola 𖹭</h1>
      <div style="display: flex;">
          <input type="text" v-model="newTask" placeholder="Add new list...">
          <button @click="addTask">Add</button>
      </div>

      <div v-for="(task, index) in incompleteTasks" :key="index" class="task" :class="{ 'completed': task.completed }">
          <input type="checkbox" v-model="task.completed" class="checkbox">
          <div v-if="!task.editing" class="task-text">{{ task.title }}</div>
          <div v-else class="edit-mode">
              <input v-model="task.title" class="edit-input">
              <div class="button-group">
                  <button class="update-btn" @click="updateTask(index)">Update</button>
                  <button class="cancel-btn" @click="cancelTask(index)">Cancel</button>
              </div>
          </div>
          <div v-if="!task.editing" class="button-group">
              <button class="edit-btn" @click="editTask(index)">Edit</button>
              <button class="delete-btn" @click="deleteTask(index)">Delete</button>
          </div>
      </div>

      <button class="filter-btn" @click="showIncomplete = !showIncomplete">
          {{ showIncomplete ? 'Show All List' : 'Show Incomplete List Only' }}
      </button>
  </div>
</template>

<script>
export default {
  data() {
      return {
          tasks: [],
          newTask: '',
          showIncomplete: true
      };
  },
  methods: {
      addTask() {
          if (this.newTask.trim() !== '') {
              this.tasks.push({ title: this.newTask, completed: false });
              this.newTask = '';
          }
      },
      cancelTask(index) {
          this.tasks[index].editing = false;
      },
      editTask(index) {
          this.tasks[index].editing = true;
      },
      updateTask(index) {
          this.tasks[index].editing = false;
      },
      deleteTask(index) {
          this.tasks.splice(index, 1);
      }
  },
  computed: {
      incompleteTasks() {
          if (this.showIncomplete) {
              return this.tasks.filter(task => !task.completed);
          } else {
              return this.tasks;
          }
      }
  }
};
</script>

<style scoped>
@media (max-width: 768px) {
    body {
      font-family:fantasy;
      background-color: #90553C;
      margin: 0;
      padding: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      font-family:cursive;
    }

    .container {
      width: 300px;
    }
  
    input[type="text"] {
      width: calc(100% - 75px);
    }
  }
  
</style>
