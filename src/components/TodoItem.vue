<template>
  <li class="list-group-item" :class="{ done: task.completed }">
    <i @click="toggleCompleted(task.id)" class="far fa-square done-icon"></i>
    <i @click="toggleCompleted(task.id)" class="far fa-check-square done-icon"></i>
    <span class="todo-text">{{ task.title }}</span>
    <i @click="handleDelete(task.id)" class="far fa-trash-alt"></i>
  </li>
</template>

<script>
export default {
  props: {
    task: Object,
    toggleCompleted: Function,
    isCompleted: Boolean,
    deleteTodo: Function
  },
  methods: {
    handleDelete (id) {
      if (confirm('Are you sure?')) this.deleteTodo(id)
    }
  }
}

</script>
