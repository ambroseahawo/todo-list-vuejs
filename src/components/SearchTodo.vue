<template>
  <form @submit="handleSubmit" class="input-group mb-3">
    <input type="text" id="search" v-model="searchText" class="form-control" placeholder="Search todo">
    <div class="input-group-append">
      <button type="submit" class="input-group-text"> <i class="fas fa-search"></i> </button>
    </div>
  </form>
</template>

<script>
export default {
  name: 'SearchTodo',
  data () {
    return {
      searchText: ''
    }
  },
  props: {
    searchTodo: Function
  },
  methods: {
    handleSubmit (e) {
      e.preventDefault()
      this.searchTodo(this.searchText)
    }
  }
}

</script>
