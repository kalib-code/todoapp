<template>
  <div id="app">
    <h1>Todos</h1>
    <input type="text" v-model="todoName" @keyup.enter="addTodo">
    <ul>
      <li v-for="todo of todos" :key="todo.id">
        {{todo.name}}
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';
const baseUrl = 'http://localhost:3000/todos'

export default {
  name: 'app',
  data() {
    return {
      todos: [],
      todoName: ''  
    }
  },
  async created() {
    try {
      const res = await axios.get(baseUrl)

      this.todos = res.data;
    } catch(e) {
      console.error(e)
    }
  },
  methods:{
    async addTodo(){
      const res = await axios.post(baseUrl, {name: this.todoName})
      this.todos = [...this.todos, res.data]
      this.todoName = ''
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #6c5ce7;
  margin-top: 60px;
}

li {
  list-style: none;
}

h1 {
  color: #a29bfe
}
</style>
