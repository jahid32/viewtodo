   <template>
    <div class="todo" :class="{'todo--done':todo.status == 'done'}" :key="todo.id">
      <div class="todo__status-dot"></div>
      <div>
        <p class="todo__content">{{todo.task}}</p>
        <small class="todo__time"> {{todo.createdAt}}</small>
      </div>
    </div>
    </template>
    <script>
   export default {
       props: ['todo'],
   }
   
    </script>
    