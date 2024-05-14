<template>
  <div>
    <h1>My To Do List</h1>
    <div class="input-container">
      <input type="text" v-model="newTask" placeholder="Tambahkan Kegiatan">
      <button @click="addTask">Tambah</button>
    </div>
    <ul>
      <li v-for="(task, index) in tasks" :key="index" class="task-item">
        <span v-if="index !== editIndex">{{ task }}</span>
        <input v-else type="text" v-model="tasks[index]">
        <div class="button-group">
          <button @click="editTask(index)" class="edit-button">{{ index !== editIndex ? 'Edit' : 'Save' }}</button>
          <button @click="removeTask(index)" class="delete-button">Delete</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: [],
      editIndex: -1
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        this.tasks.push(this.newTask);
        this.newTask = '';
      }
    },
    editTask(index) {
      if (this.editIndex === index) {
        this.editIndex = -1;
      } else {
        this.editIndex = index;
      }
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
      if (index === this.editIndex) {
        this.editIndex = -1;
      }
    }
  }
}
</script>

<style scoped>
body {
  background-image: url(https://i.pinimg.com/736x/99/38/d5/9938d5413831d7e8bb1147c35677de54.jpg);
  background-size: cover;
  background-repeat: no-repeat;
  display: flex;
  place-items: center;
  min-height: 100vh;
}

h1 {
  text-align: center;
  margin-bottom: 20px;
}

.input-container {
  margin-bottom: 10px;
}

.input-container input {
  background-color: #fff;
  color:#000000;
  margin-bottom: 10px;
  padding: 8px;
  font-size: 16px;
  width: 70%;
}

.input-container button {
  padding: 8px 15px;
  font-size: 16px;
}

ul {
  list-style-type: none;
  padding: 0;
}

.task-item {
  margin-bottom: 10px;
  display: flex;
  align-items: center;
  background-color: #000000;
  padding: 8px;
  border-radius: 5px;
}

.task-item input {
  flex-grow: 1;
  padding: 8px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.button-group {
  margin-left: auto;
}

.edit-button,
.delete-button {
  background-color:blue;
  padding: 8px 15px;
  font-size: 16px;
  border-radius: 5px;
}

.delete-button {
  background-color: #ff4d4f;
  color: #fff;
  border: none;
  margin-left: 10px;
}
</style>
