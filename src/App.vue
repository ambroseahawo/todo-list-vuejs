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
            <SearchTodo :searchTodo="searchTodo" />
            <TodosList :todos="todos" :toggleCompleted="toggleCompleted" :isCompleted="isCompleted"
              :deleteTodo="deleteTodo" />
            <button @click="deleteAllTodos" id="clearBtn" type="button" class="btn btn-dark btn-sm">Clear All</button>
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
    addTodo (todo) {
      const newTodoTitle = todo.title
      const existingTodo = this.todos.filter((todo) => todo.title === newTodoTitle)
      if (existingTodo.length === 0) {
        this.todos = [todo, ...this.todos]
      } else {
        alert(`Todo (${newTodoTitle}) already exists!`)
      }
    },
    toggleCompleted (id) {
      // this.isCompleted = !this.isCompleted
      const todoToToggle = this.todos.filter((todo) => todo.id === id)[0]
      const updatedTodo = { ...todoToToggle, completed: !todoToToggle.completed }

      this.todos = this.todos.map((todo) =>
        todo.id === id ? { ...todo, completed: updatedTodo.completed } : todo
      )
    },
    deleteTodo (id) {
      this.todos = this.todos.filter((todo) => todo.id !== id)
    },
    deleteAllTodos () {
      if (confirm('Are you sure')) this.todos = []
    },
    searchTodo (searchText) {
      if (!searchText) alert('Enter text to search')
      const result = this.todos.filter((todo) => todo.title.toLowerCase().includes(searchText.toLowerCase()))

      if (result.length > 0) {
        this.todos = result
      } else {
        alert(`${searchText} not found in your todo list`)
      }
    }
  },
  async created () {
    this.todos = [
      {
        id: 1,
        title: 'Placeholder',
        completed: false
      }
    ]
  },
  components: {
    SearchTodo,
    TodosList,
    AddTodoItem
  }
}
</script>
