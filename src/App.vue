<template>
  <div id="app">
    <Header/>
    <br>
    <CreateTodo v-on:createTodo="createTodo" />
    <div class="container">
      <Todos v-bind:todos="todos" v-on:del-todo="onCommitDelete"/>
    </div>
  </div>
</template>

<script>
import Todos from './components/Todos';
import Header from './components/layout/Header';
import CreateTodo from './components/CreateTodo';
import axios from 'axios';

export default {
  name: 'app',
  components: {
    Todos,
    Header,
    CreateTodo,
  },
  data(){
    return {
      todos:[]
    }
  },
  methods:{
    onCommitDelete(id) {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(res => this.todos = this.todos.filter(todo => todo.id !== id))
      .catch(err => console.log(err))
     
    },
    createTodo(newTodo) {
      const { title, completed } = newTodo;

      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        completed
      }).then(res =>  this.todos = [...this.todos, res.data])
        .catch(err => console.log(err));

     
    },
  },
  created() {
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=10')
          .then(res => this.todos = res.data)
          .catch(err => console.log(err));
  }
}
</script>

<style>
body {
  font-family: Arial, Helvetica, sans-serif;
  margin: auto;
}

.container {
  margin: auto;
  width: 60%;
  display: flex;
}

</style>
