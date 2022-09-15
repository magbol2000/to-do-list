<script>
let id = 0

export default {
  data() {
    return {
      hiddenClass: "hidden",
      newTodo: '',
      isNotEdit: true,
      todoTemp: '',
      todos: [
        { id: id++, text: 'Learn HTML' },
        { id: id++, text: 'Learn JavaScript' },
        { id: id++, text: 'Learn Vue' }
      ]
    }
  },
  methods: {
    addTodo() {
      this.todos.push({ id: id++, text: this.newTodo })
      this.newTodo = ''
    },
    removeTodo(todo) {
      this.todos = this.todos.filter((t) => t !== todo)
    },
    preUpdateTodo(todo) {
      this.newTodo = todo.text
      this.todoTemp = todo
      this.isNotEdit = false
    },
    updateTodo() {
      this.todos.find(item => item === this.todoTemp).text = this.newTodo;
      this.newTodo = ''
      this.isNotEdit = true

    }
  }
}
</script>

<template>
  <div>
    <input v-model="newTodo">
    <button v-if="isNotEdit" @click="addTodo">Add Todo</button>
    <button v-else @click="updateTodo">Edit the Todo</button>
  </div>
  <ul>
    <li v-for="todo in todos" :key="todo.id">
      {{ todo.text }}
      <button v-if="isNotEdit" @click="preUpdateTodo(todo)">✎</button>
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
</template>