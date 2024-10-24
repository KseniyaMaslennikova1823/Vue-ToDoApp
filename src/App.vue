<template>
  <div class="app">
    <Header />
    <Filterlist  :activeFilter="activeFilter" @setFilter="setFilter"/>
    <NewTask @addTask="addTask" />
    <ListTasks 
      :tasks="filteredTasks"
      @toggleTask="toggleTask" 
      @deleteTask="deleteTask" 
      @updateTask="updateTask"
    />
  </div>
</template>

<script lang="ts">
import { ref, defineComponent } from 'vue'
import Header from "./components/Header.vue";
import Filterlist from "./components/filterList.vue";
import NewTask from "./components/newTask.vue";
import ListTasks from "./components/listTasks.vue";
import { Task } from "./components/Task.ts";

export default defineComponent({
components: {
        Header,
        Filterlist,
        ListTasks,
        NewTask
    },
  data() {
    return {
      tasks: [
          {id: 0, title: 'Задача 1', text: 'Описание 1', status: true},
          {id: 1, title: 'Задача 2', text: 'Описание 2', status: false},
          {id: 2, title: 'Задача 3', text: 'Описание 3', status: false},
      ],
      activeFilter: 'Все',
    }
  },
  computed: {
    filteredTasks(activeFilter: String) {
      switch (this.activeFilter) {
        case 'Активные':
          return this.tasks.filter(task => !task.status)
        case 'Завершенные':
          return this.tasks.filter(task => task.status)
        case 'Все':
        default:
          return this.tasks
      }
    }
  },
  methods: {
    toggleTask(id: Number) {
        const taskStatus = this.tasks.find(task => task.id === id)
        if(taskStatus) {
            taskStatus.status = !taskStatus.status
        }
    },
    deleteTask(id: Number) {
        this.tasks = this.tasks.filter(task => task.id !== id)
    },
    addTask(task: Object) {
      this.tasks.push(task)
    },
    setFilter(filter: String) {
      this.activeFilter = filter
    },
    updateTask(id: Number, taskTitle: String, taskText: String) {
      const updateTasks = this.tasks.find(task => task.id === id)
      updateTasks.title = taskTitle
      updateTasks.text = taskText
    }
  },
})
</script>

<style lang="scss">
.app {
  box-shadow: 0px 0px 50px rgba(#36D986, 1);
  width: 600px;
  margin: 100px auto;
  border-radius: 25px;
  padding: 10px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
