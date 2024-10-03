<template>
    <ul class="list">
        <Tasks
            v-for="task in tasks" 
            :key="task.id" 
            :task="task" 
            @toggleTask="toggleTask"
            @deleteTask="deleteTask"
            @updateTask="updateTask"
        />
    </ul>
</template>

<script lang="ts">
import { PropType, defineComponent } from 'vue'
import Tasks from "./task.vue";
import { Task } from './Task.ts';


export default defineComponent({
    components: {
        Tasks
    },
    props: {
        tasks: Array as PropType<Task[]> 
    },

  methods: {
    toggleTask(id) {
        this.$emit('toggleTask', id)
    },
    deleteTask(id) {
        this.$emit('deleteTask', id)
    },
    updateTask(id, taskTitle, taskText) {
        this.$emit('updateTask', id, taskTitle, taskText)
    }
  }
})
</script>

<style lang="scss">
.list {
    list-style: none;
    width: 90%;
    margin-top: 10px;
  
}
</style>
