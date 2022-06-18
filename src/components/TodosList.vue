<template>
  <ul class="list-group mb-3">
    <!-- todo item component -->
    <TodoItem
      v-for="task in todos"
      :key="task.id"
      :task="task"
      :toggleCompleted="toggleCompleted"
      :isCompleted="isCompleted"
      :deleteTodo="deleteTodo"
    />
  </ul>
</template>

<script>
import TodoItem from '@/components/TodoItem.vue'

export default {
  name: 'TodosList',
  props: {
    todos: Array,
    toggleCompleted: Function,
    isCompleted: Boolean,
    deleteTodo: Function
  },
  components: {
    TodoItem
  }
}

</script>
