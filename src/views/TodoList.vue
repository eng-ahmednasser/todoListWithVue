<template>
  <div id="app">
    <AddTodo v-on:new-todo="addTodo"/>
    <Todos v-bind:todos="todoList" v-on:delete-todo="deleteTodo" />
  </div>
</template>

<script>
import Todos from '../components/Todos.vue'
import Header from '../components/layout/Header.vue';
import AddTodo from '../components/AddTodo.vue';

import axios from 'axios';

export default {
  name: 'TodoList',
  components: {
    AddTodo,
    Header,
    Todos
  },
  data(){
    return {
      todoList:[]
    }
  },
  methods:{
    deleteTodo(id){
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(response=>this.todoList=this.todoList.filter(todo => todo.id != id))
      .catch(err => console.log(err));
    },
    addTodo(newTodo){
      const {title , completed}= newTodo;
      axios.post('https://jsonplaceholder.typicode.com/todos',{
        title,
        completed
      })
      .then(response=>this.todoList = [...this.todoList ,response.data])
      .catch(err => console.log(err));
      
      
    }

  },
  created(){
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=15')
    .then(response =>this.todoList=response.data)
    .catch(error => console.log(error))
  }
}
</script>

<style >
/* #app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 0px;
} */
 * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }
  .btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }
  .btn:hover {
    background: #666;
  }
</style>
