<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    
    <form @submit.prevent="addNewTodo">
      <label>New Todo</label>
      <input name="newtodo" v-model="newTodo">
      <button> Add </button>
    </form>
    
    <button @click="removeAll()">Remove All Todos</button>
    <button @click="markAllDone()">Mark All Done</button>

    <ul>
      <li v-for="(todo, index) in todos" :key="todo.id">
        <h3 :class="{ done: todo.done }" @click="toggleDone(todo)"> {{ todo.content }} </h3>
        <button @click="removeTodo(index)"> Remove </button>
      </li>
    </ul>

  </div>
</template>

<script>

import { ref } from 'vue';

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  setup() {
    const newTodo = ref('');
    const todos = ref([]);

    function addNewTodo() {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value
      });

      newTodo.value = "";
    }

    function toggleDone(todo) {
      todo.done = !todo.done; 
    }

    function removeTodo(index) {
      todos.value.splice(index, 1);
    }

    function markAllDone() {
      todos.value.forEach(todo => todo.done = true);
    }

    function removeAll() {
      todos.value = [];
    }

    return {
      newTodo,
      todos,
      addNewTodo,
      toggleDone,
      removeTodo,
      markAllDone,
      removeAll
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
  cursor:  pointer;
}
a {
  color: #42b983;
}

.done {
  text-decoration: line-through;
}
</style>
