<template>
  <div class="container">
    <div class="row">
      <div class="col-lg-5 col-md-6 col-sm-8 mx-auto">
        <div class="card my-5">
          <h5 class="card-header bg-primary text-white">
            Todo List
          </h5>
          <div class="card-body">
            <!-- search component -->
            <SearchTodo />
            <ul class="list-group mb-3">
              <!-- todo item component -->
              <TodoItem
                :toggleCompleted="toggleCompleted"
                :isCompleted="isCompleted"
              />
            </ul>
            <button id="clearBtn" type="button" class="btn btn-dark btn-sm">Clear All</button>
          </div>
          <!-- add todo item component -->
          <AddTodoItem />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import SearchTodo from '@/components/SearchTodo.vue'
import TodoItem from '@/components/TodoItem.vue'
import AddTodoItem from '@/components/AddTodoItem.vue'

export default {
  data () {
    return {
      isCompleted: false,
      todos: []
    }
  },
  methods: {
    async fetchTodos () {
      const res = await fetch('api/todos')
      const data = await res.json()
      return data
    },
    toggleCompleted () {
      this.isCompleted = !this.isCompleted
    }
  },
  async created () {
    this.todos = await this.fetchTodos()
  },
  components: {
    SearchTodo,
    TodoItem,
    AddTodoItem
  }
}
</script>

<style>
</style>
