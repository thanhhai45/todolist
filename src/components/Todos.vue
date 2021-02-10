<template>
  <div>
    <AddTodo @add-item="addTodo" />
    <TodoItem 
      v-for="todo in todos"
      :key="todo.id"
      :item="todo"
      @item-completed="markComplete"
      @delete-item="deleteTodo"
    />
  </div>  
</template>


<script>
import { ref } from 'vue'
import axios from 'axios'
import TodoItem from './TodoItem'
import AddTodo from './AddTodo'

export default {
  name: 'Todos',
  components: { TodoItem, AddTodo },
  setup() {
    const todos = ref([])

    const getAllTodos = async () => {
      try {
        const res = await axios.get(
          'https://jsonplaceholder.typicode.com/todos?_limit=10'
        )
        todos.value = res.data
      } catch (error) {
        console.error(error)
      }
    }

    const markComplete = id => {
      todos.value = todos.value.map(todo => {
        if (todo.id === id) {
          todo.completed = !todo.completed
        }
        return todo
      })
    }

    const deleteTodo = async id => {
      try {
        await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        todos.value = todos.value.filter(todo => todo.id !== id)
      } catch (error) {
        console.error(error)
      }
      
    }

    const addTodo = async newItem => {
      try {
        const res = await axios.post('https://jsonplaceholder.typicode.com/', newItem)
        todos.value.push(res.data)
      } catch (error) {
        console.error(error)
      }
      todos.value.push(newItem)
    }
    getAllTodos()
    return {
      todos,
      markComplete,
      deleteTodo,
      addTodo,
      getAllTodos
    }
  }
}
</script>

<style>

</style>