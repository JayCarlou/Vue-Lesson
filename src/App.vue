<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/> -->
      <Header/>
      <AddTodo v-on:add-todo="addTodo"/>
      <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import Todos from './components/Todos.vue';
import AddTodo from './components/AddTodo.vue';
import Header from './components/layout/header.vue';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    Todos,
    Header,
    AddTodo
  },
  data(){
    return{
      todos : [
        // {
        //   id: 1,
        //   title: "Todo One",
        //   completed: false,
        // },
        // {
        //   id: 2,
        //   title: "Todo Two",
        //   completed: true,
        // },
        // {
        //   id: 3,
        //   title: "Todo Three",
        //   completed: false,
        // }
      ]
    }
  },
  methods:{
    deleteTodo(id){
      //this.todos = this.todos.filter(todo => todo.id !== id)
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(res => {
        this.todos = this.todos.filter(todo => todo.id !==id)
        return res
      })
      .catch(error => {
        return Promise.reject(error);
      })

    },
    addTodo(newTodo){
      const {title, completed} = newTodo;
      axios.post('https://jsonplaceholder.typicode.com/todos',{
        title,
        completed
      })
      .then(res => this.todos = [...this.todos, res.data])
      .catch(error => {
        return Promise.reject(error);
      })

      //this.todos = [...this.todos, newTodo]
    }
  },
  
  created(){
    axios.get('https://jsonplaceholder.typicode.com/todos')
    .then(res => this.todos = res.data)
    .catch(error =>{
      return Promise.reject(error);
    })
  }
}
</script>

<style>
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body{
  font-family: Arial, Helvetica, sans-serif;
}

.btn{
  display: inline;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}
.btn:hover{
  background: rgb(27, 27, 27);
}
</style>
