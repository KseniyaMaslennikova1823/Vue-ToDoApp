<template>
    <div class="filters">
        <section class="filters__group">
            <button 
                v-for="filter in filters"
                :key="filter"
                class="filters__group__btn" 
                :class="{'btn-active': activeFilter === filter}"
                @click="setFilter(filter)"
            > {{ filter }} </button>
        </section>
    </div>
</template>

<script lang="ts">
import { PropType, defineComponent } from 'vue'

export default defineComponent({
    props: {
        activeFilter: {
            type: String as PropType<'Все' | 'Активные' | 'Завершенные'>,
            required: true,
        }
    },

  data() {
    return {
        filters: ['Все', 'Активные', 'Завершенные']
    }
  },
  methods: {
    setFilter(filter) {
        this.$emit('setFilter', filter)
    }
  },
})
</script>

<style lang="scss">
.filters {

    width: 100%;
    margin-top: 15px;

    &__group {
        display: flex;
        justify-content: space-around;

        &__btn {
            border-radius: 25px;
            font-size: 40px;
            padding-left: 20px;
            padding-right: 20px;
        }
    }
}
.btn-active {
    border: 1px solid #36D986;
}
</style>
