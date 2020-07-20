<template>
  <div id="app">
 
    <addTodo v-on:add-todo="addTodo"/>
        <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>   
  </div>
</template>

<script>

import Todos from '../components/Todos';
import addTodo from '../components/addTodo';
import axios from 'axios';
export default {
  name: 'Home',
  components: {
   
        Todos,
        addTodo

  },
  data() {
    return{
    todos: [ ]
  }
},
methods:{
      deleteTodo(id){
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
   
      .then(res => this.todos = this.todos.filter(todo => todo.id !==id))
      .catch(err =>console.log(err));     
    },

    addTodo(newTodo){
      const {title, completed} = newTodo;
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        completed
        })
        .then(res => this.todos = [...this.todos, res.data])
        .catch(err => console.log(err));
      
    }
  },
  //runs right away-this is where we run our request you can use fetch API 
  //instead of axios(npm install axios)-an HTTP library to get request,etc
  created(){
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')//returns a promise and we
        .then(res => this.todos = res.data)//gives us a response 
        .catch(err => console.log(err));

  }
}
</script>

<style>
    *{
      box-sizing: border-box;
      margin: 0;
      padding:0;
    }
    body{
      font-family: Arial, Helvetica, sans-serif;
      line-height: 1.4;
    }
    .btn{
      display: inline-block;
      border:none;
      background:#555;
      color:#fff;
      padding: 7px 20px;
      cursor: pointer;
    }
    
    </style>
