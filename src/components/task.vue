<template>
    <li class="list__item"  >
        <div class="list__item__status">
            <button class="list-stroke list-done" @click="toggleTask">
                <i class="fa-solid fa-check" style="color: #007439; font-size: 30px;"></i>
            </button>
        </div>
        <div class="list__item__info" :class="{'list-item-done': task.status}" >
            <p class="list__item__info__title"> {{ task.title }} </p>
            <p class="list__item__info__text"> {{ task.text }} </p>
        </div>
        <form class="updateForm" v-if="visibleFormUp" :task="task">
            <input class="updateForm__input" v-model="taskTitle" />
            <textarea class="updateForm__textarea" v-model="taskText" />
            <div class="updateForm__control">
                <button class="updateForm__control__btn" @click="closeForm">Отменить</button>
                <button class="updateForm__control__btn" @click.prevent="updateTask">Сохранить</button>
            </div>
        </form>
        <button v-else class="list__item__update" @click="showForm">
            <i class="fa-solid fa-pencil" style="color: #007439; font-size: 30px;"></i>
        </button> 
        <button class="list__item__delete" @click="deleteTask">
            <i class="fa-solid fa-trash" style="color: #007439;font-size: 30px;"></i>
        </button>            
    </li>
</template>

<script lang="ts">
import { PropType, defineComponent } from 'vue'
import { Task } from "./Task.ts";

export default defineComponent({
    props: {
        task: {
            type: Object as PropType<{Task}>,
            required: true,
        }
    },
    data() {
    return {
        visibleForm: true,
        visibleFormUp: false,
        taskTitle: this.task.title,
        taskText: this.task.text
    }
  },
    methods: {
        toggleTask(id: Number) {
            this.$emit('toggleTask', this.task.id)
        },
        deleteTask(id: Number) {
            this.$emit('deleteTask', this.task.id)
        },
        showForm() {
            this.visibleFormUp = true
        },
        closeForm() {
            this.visibleFormUp = false
        },
        updateTask(id: Number) {
            this.visibleFormUp = false,
            this.$emit('updateTask', this.task.id, this.taskTitle, this.taskText)
        }
    }
})
</script>

<style lang="scss">
    .list__item {
        border: 1px solid #62D99C;
        padding:10px;
        display: flex;
        justify-content: space-between;
        align-items: center;
        font-size: 35px;
        margin: 5px 0;
        border-radius: 15px;
        &__status {
            width: 50px;
            height: 50px;
        }
        &__info {
            width: 75%;
            &__title {
                font-size: 35px;
            }
            &__text {
                font-size: 30px;
            }
        }
        &__update {
            width: 50px;
            height: 50px;
        }
        &__delete {
            width: 50px;
            height: 50px;
        }
    }
    .list-item-done {
        text-decoration: line-through;
    }
.updateForm {
    z-index: 10;
    position: absolute;
    background-color: white;
    width: 540px;
    border-radius: 25px;
    padding: 10px;
    display: flex;
    flex-direction: column;
    align-items: center;
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
    &__control {
        width: 100%;
        display: flex;
        justify-content: space-around;
        margin-top: 10px;
        &__btn {
            font-size: 45px;
            margin-bottom: 15px;
        }
    }
}
</style>
