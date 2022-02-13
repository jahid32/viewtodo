<template>
<div class="app-container">
  <h1 class="app-title">Vuejs todos</h1>

  <div class="composer">
    <form @submit.prevent="addTodo"> 
    <input type="text" v-model="newTodo" placeholder="Type and hit enter..." class="composer__input" />
    </form>
    <div class="filter">
      <div class="filter__left">
        <button class="filter__button filter__button--active">All ({{todosCount}})</button>
        <button class="filter__button">Pending ({{pendingCount}})</button>
        <button class="filter__button">Done ({{doneCount}})</button>
      </div>
      <div>
        <button class="filter__button filter__button--danger">Clear</button>
      </div>
    </div>
  </div>

  <div class="todos">
    <!-- Todo start -->
    <Todo v-for="todo in todos" :key="todo.id" :todo="todo" />  
    <!-- Todo end -->

  </div>
</div>
</template>

<script>
import { v4 as uuidv4 } from 'uuid';
import Todo from './components/Todo.vue';
import { computed } from '@vue/runtime-core';
export default {
  name: 'Todo App',
  components: {
    Todo
  },
  data() {
    return {
      newTodo: '',
      todos: []
    }
  },
  methods: {
    addTodo() {
      this.todos.push({
        id: uuidv4(),
        task: this.newTodo,
        status: "pending",
        createdAt: new Date().toString()
      });
      this.newTodo = '';
    }
  },
  computed: {
    todosCount() {
      return this.todos.length;
    },
    pendingCount() {
      return this.todos.filter(todo => todo.status === 'pending').length;
    },
    doneCount() {
      return this.todos.filter(todo => todo.status === 'done').length;
    }
  }
}
</script>