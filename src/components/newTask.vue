<template>
    <div class="addTask">
        <form 
            v-if="visibleForm" 
            class="addTask__form" 
            @submit.prevent="addTask"
        >
            <button class="addTask__form__closeForm" @click="closeForm">Закрыть</button>
            <input v-model="taskTitle" class="addTask__form__input" placeholder="Название задачи" />
            <textarea v-model="taskText" class="addTask__form__textarea" placeholder="Описание задачи" />
            <button class="addTask__form__submit">Добавить</button>
        </form>
        <button v-else class="addTask__showForm" @click="showForm">Новая задача</button>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({

  data() {


    return {
        visibleForm: false,
        taskTitle: '',
        taskText: '',
    }
  },
  methods: {
    showForm() {
        this.visibleForm = true
    },
    closeForm() {
        this.visibleForm = false
    },
    addTask() {
        this.$emit('addTask', {
            id: Date.now(),
            title: this.taskTitle,
            text: this.taskText,
            status: false
        })

        this.taskTitle = '',
        this.taskText = ''
    }
  },
})
</script>

<style lang="scss">
.addTask {
    width: 90%;
    display: flex;
    flex-direction: column;
    align-items: center;
    &__showForm {
        font-size: 35px;
        

    }
    &__form {
        width: 100%;
        display: flex;
        flex-direction: column;
        align-items: center;

        &__closeForm {
            font-size: 45px;
        }
        &__input {
            width: 90%;
            font-size: 45px;
            border-radius: 25px;
            padding: 10px;
            border: 1px solid #36D986;
            outline: none;
        }
        &__textarea {
            width: 90%;
            font-size: 35px;
            border-radius: 25px;
            padding: 10px;
            border: 1px solid #36D986;
            margin-top: 10px;
            outline: none;
        }
        &__submit {
            font-size: 45px;
            margin-bottom: 15px;
        }
    }
}
</style>
