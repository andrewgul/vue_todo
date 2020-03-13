<template>
    <div>
        <ul>
            <TodoItem 
                v-for="(todo, i) of todos" :key="todo.id"
                v-bind:todo="todo"
                v-bind:index="i"
                v-on:remove-todo="removeTodo"
            />
        </ul>
    </div>
</template>

<script>
import TodoItem from '@/components/TodoItem'
export default {
    props: [
        'todos'
    ],
    methods: {
        removeTodo(id){
            this.$emit('remove-todo', id)
        }
    },
    components: {
        TodoItem
    }
}
</script>

<style>
    ul {
        list-style-type: none;
        padding: 0;
        margin: 0;
    }
</style>