<template>
  <div class="card-footer">
    <form @submit="onSubmit" id="form">
      <div class="input-group">
        <input type="text" v-model="title" class="form-control" id="todo" placeholder="Add new todo item">
        <div class="input-group-append">
          <button type="submit" class="btn btn-primary"><i class="fas fa-plus"></i> Add
          </button>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: 'AddTodoItem',

  data () {
    return {
      title: ''
    }
  },
  props: {
    addTodo: Function
  },
  methods: {
    onSubmit (e) {
      e.preventDefault()

      console.log(this.title.length)

      if (!this.title) {
        alert('Please add a task')
        return false
      } else {
        if (this.title.length <= 20) {
          const newTodo = {
            id: Math.floor(Math.random() * 100000),
            title: this.title.toLowerCase(),
            completed: false
          }
          this.addTodo(newTodo)

          this.title = ''
        } else {
          alert('Todo title should not exceed 20 characters')
        }
      }
    }
  }
}

</script>
