<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import Todos from '../components/Todos';
import AddTodo from '../components/AddTodo';
import axios from 'axios';

export default {
  name: 'Home',
  components: {
    Todos,
    AddTodo
  },
  data () {
    return {
      todos: [
        // {
        //   id: 1, title: "Todo #01", completed: false
        // },{
        //   id: 2, title: "Todo #02", completed: false
        // },{
        //   id: 3, title: "Todo #03", completed: false
        // }
      ]
    }
  },
  methods: {
    deleteTodo: function(id){
      axios.delete('https://jsonplaceholder.typicode.com/todos/' + id)
      .then(res => {
        this.todos = this.todos.filter(todo => todo.id !== id),
        console.log(res.data)
      })
      .catch(error => console.log(error));

      // Filter is high order array method
      // this.todos = this.todos.filter(todo => todo.id !== id);
    },
    addTodo: function(newTodo){
      const { title, completed } = newTodo;
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title, completed
      })
      .then(res => this.todos = [ res.data, ...this.todos ])
      .catch(err => console.log(err))
      // Inserting newTodo in the array which has already existing.
      // this.todos = [...this.todos, newTodo]; // Not using now. Coz axios is using
    }
  },
  // When component loads created() will be called
  created() {
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=10')
    .then(res => this.todos = res.data)
    .catch(err => console.log(err))
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}
</style>
