<template>
  <h1>Vue 3 Todo APP</h1>
  <form @submit.prevent="addNewTodo">
    <label>New Todo</label>
    <input v-model="newTodo" name="newTodo">
    <button>Add New Todo</button>
    <button @click="removeAllTodos">Remove all</button>
    <button @click="markAllDone">Mark all done</button>
  </form>
  
  <ul>
    <li v-for="todo, index in todos" :key="todo.id"  class="todo">
      <h3 :class="{ done: todo.done }" @click="toggleDone(todo)"> {{todo.content}} </h3>
      <button @click="removeTodo(index)">Remove Todo</button>
  </li>
  </ul>
</template>


<script>
import { reactive, ref } from 'vue'


  export default {
     setup() {
      const newTodo = ref('')
      const todos = ref([])



      function addNewTodo() {
        todos.value.push({
          id: Date.now(),
          done: false,
          content: newTodo.value,
        })
        newTodo.value = ''
        
      }

      function toggleDone(todo) {
        todo.done = !todo.done
      }

      function removeTodo(index) {
        todos.value.splice(index, 1)
      }

      function markAllDone() {
        todos.value.forEach((todo) => todo.done = true)
      }

      function removeAllTodos() {
        todos.value = [];
      }

      return {
        todos,
        newTodo,
        addNewTodo,
        toggleDone,
        removeTodo,
        markAllDone,
        removeAllTodos,
      }

     }
  }
</script>



<style scoped>
  body {
  font-family: sans-serif;
  padding-top: 1em;
  padding-bottom: 1em;
  font-size: 2em;
  width: 80%;
  margin: 0 auto;
}

form button {
  background-color: antiquewhite;
}

ul button {
  background-color: beige;
}
input, textarea, button, p, div, section, article, select {
  display: 'block';
  width: 100%;
  font-family: sans-serif;
  font-size: 1em;
  margin: 0.5em;
}

h1 {
  font-size: 40px;
  color: green;
}

h3{
  font-size: 30px;
  color: black;
}

.todo {
  cursor: pointer;
}

.done {
  text-decoration: line-through;
}
</style>
