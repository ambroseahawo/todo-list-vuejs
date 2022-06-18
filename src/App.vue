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
            <TodosList
              :todos="todos"
              :toggleCompleted="toggleCompleted"
              :isCompleted="isCompleted"
              :deleteTodo="deleteTodo"
            />
            <button id="clearBtn" type="button" class="btn btn-dark btn-sm">Clear All</button>
          </div>
          <!-- add todo item component -->
          <AddTodoItem :addTodo="addTodo" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import SearchTodo from '@/components/SearchTodo.vue'
import AddTodoItem from '@/components/AddTodoItem.vue'
import TodosList from '@/components/TodosList.vue'

export default {
  data () {
    return {
      isCompleted: false,
      todos: []
    }
  },
  // method declarations should be procedural, don't call before declaring above
  methods: {
    async addTodo (todo) {
      const res = await fetch('api/todos', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json'
        },
        body: JSON.stringify(todo)
      })

      const data = await res.json()
      this.todos = [...this.todos, data]
    },
    async fetchTodos () {
      const res = await fetch('api/todos')
      const data = await res.json()
      return data
    },
    async fetchTodo (id) {
      const res = await fetch(`api/todos/${id}`)
      const data = await res.json()
      return data
    },
    async toggleCompleted (id) {
      // this.isCompleted = !this.isCompleted
      const todoToToggle = await this.fetchTodo(id)
      const updatedTodo = { ...todoToToggle, completed: !todoToToggle.completed }

      const res = await fetch(`api/todos/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json'
        },
        body: JSON.stringify(updatedTodo)
      })

      const data = await res.json()

      this.todos = this.todos.map((todo) =>
        todo.id === id ? { ...todo, completed: data.completed } : todo
      )
    },
    async deleteTodo (id) {
      const res = await fetch(`api/todos/${id}`, {
        method: 'DELETE'
      })

      res.status === 200
        ? (
            this.tasks = this.todos = this.todos.filter((todo) => todo.id !== id)
          )
        : alert(
          'Error deleting todo, please try again'
        )
    }
  },
  async created () {
    this.todos = await this.fetchTodos()
  },
  components: {
    SearchTodo,
    TodosList,
    AddTodoItem
  }
}
</script>
