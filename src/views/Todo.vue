<template>
  <div>
    <AddTodo 
      @add-todo="addTodo"
    />
    <select v-model="filter">
        <option value="all">All</option>
        <option value="completed">Completed</option>
        <option value="not-completed">Not completed</option>
    </select>
    <TodoList 
      v-if="filteredTodos.length"
      v-bind:todos="filteredTodos"
      @remove-todo="removeTodo"
    />
    <p v-else>No todos yet!</p>
    <router-link to="/">GO BACK</router-link>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList'
import AddTodo from '@/components/AddTodo'
import Loader from '@/components/Loader'
export default {
  data() {
    return {
      todos: [],
      loading: true,
      filter: 'all'
    }
  },
  mounted(){
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
      .then(response => response.json())
      .then(json => {
        this.todos = json
        this.loading = false
      })
  },
  computed: {
      filteredTodos(){
          if (this.filter === 'all'){
              return this.todos
          }
          if (this.filter === 'completed'){
              return this.todos.filter(t => t.completed)
          }
          if (this.filter === 'not-completed'){
              return this.todos.filter(t => !t.completed)
          } 
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
    AddTodo,
    Loader
  }
}
</script>