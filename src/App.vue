<template>
<div class="app-container">
  <h1 class="app-title">Vuejs todos</h1>

  <Composer v-model="newTodo" @onEnter="addTodo"/>
    <div class="filter">
      <div class="filter__left">
        <button class="filter__button filter__button--active" @click="filtermode ='all'">All ({{todosCount}})</button>
        <button class="filter__button" @click="filtermode ='pending'">Pending ({{pendingCount}})</button>
        <button class="filter__button" @click="filtermode ='done'">Done ({{doneCount}})</button>
      </div>
      <div>
        <button class="filter__button filter__button--danger" @click="clearTodo">Clear</button>
      </div>
    </div>
  <div class="todos">
    <!-- Todo start -->
    <Todo v-for="todo in filterTodos" :key="todo.id" :todo="todo" @doneTodo="completeTodo(todo)"/>  
    <!-- Todo end -->

  </div>
</div>
</template>

<script>
import { v4 as uuidv4 } from 'uuid';
import Todo from './components/Todo.vue';
import Composer from './components/Composer.vue';
export default {
  name: 'Todo App',
  components: {
    Todo,
    Composer
  },
  mounted() {
    this.fetchTodos();
  },
  updated() {
    localStorage.setItem('todos', JSON.stringify(this.todos));
  },
  data() {
    return {
      newTodo: '',
      todos: [],
      filtermode:'all',

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
    },
    completeTodo(todo) {
      todo.status = todo.status === 'pending' ? 'done' : 'pending';
    },
    clearTodo() {
      this.todos = this.todos.filter(todo => todo.status !== 'done');
    },
    fetchTodos() {
      const todos = localStorage.getItem('todos');
      if (todos) {
        this.todos = JSON.parse(todos);
      }
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
    },
    filterTodos() {
      if (this.filtermode === 'all') {
        return this.todos;
      } else if (this.filtermode === 'pending') {
        return this.todos.filter(todo => todo.status === 'pending');
      } else if (this.filtermode === 'done') {
        return this.todos.filter(todo => todo.status === 'done');
      }
    }
  }
}
</script>