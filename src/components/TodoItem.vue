<template>
  <li class="list-group-item" :class="{ done: isCompleted }">
    <i @click="toggleCompleted" class="far fa-square done-icon"></i>
    <i @click="toggleCompleted" class="far fa-check-square done-icon"></i>
    <span class="todo-text">Dummy Todo Item</span>
    <i class="far fa-trash-alt"></i>
  </li>
</template>

<script>
export default {
  props: ['toggleCompleted', 'isCompleted']
}

</script>
