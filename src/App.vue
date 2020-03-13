<template>
  <div id="app">
    <h1>ТУДУШЕЧКА</h1>
    <AddTodo 
      @add-todo="addTodo"
    />
    <TodoList 
      v-bind:todos="todos"
      @remove-todo="removeTodo"
    />
  </div>
</template>

<script>
import TodoList from '@/components/TodoList'
import AddTodo from '@/components/AddTodo'
export default {
  data() {
    return {
      todos: [
        {id: 1, title: "Помыть кошку", completed: false},
        {id: 2, title: "Сходить в шарагу", completed: false},
        {id: 3, title: "Купить гараж", completed: false},
      ]
    }
  },
  methods: {
    removeTodo(id){
      this.todos = this.todos.filter(t => t.id !==id)
    },
    addTodo(todo){
      this.todos.push(todo)
    }
  }, 
  name: 'App',
  components: {
    TodoList,
    AddTodo
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
