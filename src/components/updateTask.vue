<template>
    <form class="updateForm" v-if="visibleForm" :task="task">
        <input class="updateForm__input" />
        <p>{{ task.title }}</p>
        <textarea class="updateForm__textarea" />
        <div class="updateForm__control">
            <button class="updateForm__control__btn" @click="closeForm">Отменить</button>
            <button class="updateForm__control__btn" @click.prevent="updateTask">Сохранить</button>
        </div>
    </form>
    <button v-else class="list__item__update" @click="showForm">	&#9998;</button>      
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
    data() {
        return {
            visibleForm: false
        }
    },
    methods: {
        showForm() {
            this.visibleForm = true
        },
        closeForm() {
            this.visibleForm = false
        },
        updateTask(id: Number, taskTitle: String, taskText: String) {
        }
    },
})
</script>

<style lang="scss">
.list__item {
    &__update {
        border: 1px solid black;
        width: 50px;
        height: 50px;
    }
}
.updateForm {
    border: 1px solid black;
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
