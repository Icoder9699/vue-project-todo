<template>
    <ul>
        <todo-item
            v-for="(todo, i) in todos"
            :key="todo.id"
            :todo="todo"
            :index="i"
            @removeTodo="removeTodo"
            @completeTodo="completeTodo"
        />
    </ul>
</template>
<script>
import TodoItem from './TodoItem.vue'
export default {
    // * reg components
    components: {
        TodoItem
    },
    // * reg props
    props: {
        todos: {
            type: Array,
            required: true
        }
    },
    methods: {
        removeTodo(id){
            this.$emit('removeTodo', id)
        },
        completeTodo(id){
            this.$emit('completeTodo', id)
        }
    }
}
</script>
<style scoped>
    ul{
        margin: 0;
        padding: 0;
        list-style-type: none;
    }
</style>