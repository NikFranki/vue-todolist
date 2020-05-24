<template>
  <div class="todolist">
    <div>
      <input
        type="text"
        class="todo-input"
        v-model="newTodo"
        value
        placeholder="please input your focus todo today!"
      />
      <button @click="addTodo">add</button>
    </div>
    <ul>
      <li
        class="list-item"
        :class="{ active: todo.completed }"
        v-for="(todo, index) in filteredTodos"
        :key="todo.id"
        @click="select(index)"
      >{{ todo.id+1 }} {{ todo.title }}</li>
    </ul>
    <div>
      <button @click="filter('all')">all</button>
      <button @click="filter('active')">Active</button>
      <button @click="filter('completed')">Completed</button>
    </div>
  </div>
</template>

<script>
// visibility filters
const filters = {
  all: function(todos) {
    return todos
  },
  active: function(todos) {
    return todos.filter(function(todo) {
      return !todo.completed
    })
  },
  completed: function(todos) {
    return todos.filter(function(todo) {
      return todo.completed
    })
  }
}
export default {
  name: 'HelloWorld',
  data() {
    return {
      visibility: 'all',
      newTodo: '',
      id: 0,
      todos: []
    }
  },
  methods: {
    addTodo() {
      if (!this.newTodo) {
        alert('not allow submit empty value!')
        return
      }
      const item = {
        id: this.id++,
        title: this.newTodo,
        completed: false
      }
      this.todos.push(item)
      this.newTodo = ''
    },
    select(selIndex) {
      this.todos.map((item, index) => {
        if (selIndex === index) {
          item.completed = !item.completed
        }
      })
    },
    filter(type) {
      this.visibility = type
    }
  },
  computed: {
    filteredTodos: function() {
      return filters[this.visibility](this.todos)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
  font-size: 16px;
}
.todo-input {
  width: 500px;
  text-indent: 10px;
  padding: 10px 0;
  font-size: 20px;
}

ul li {
  list-style: none;
}

li.active {
  text-decoration: line-through;
}
</style>
