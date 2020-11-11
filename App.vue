<!-- It has 2 childs: 1)AddTodo 2)Todos 
and one layout 'Header'-->
<template>
  <div id="app">
    {{msg}}
    <Header />
    <!-- 'add-todo' comes from 'AddTodo.vue' and is sent using 'emit' -->
    <!-- Every time newTodo is created, "addTodo" function is called and "newTodo" is automatically passed as argument -->
    <AddTodo v-on:add-todo="addTodo" />
    <!-- "v-bind" is a template directive -->
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/> 
    <!-- We are passing "todo" from data function -->
  </div>
</template>



<script>
//get rid of the import 'Hello World'
import Header from './components/layout/Header';
import Todos from './components/Todos';
import AddTodo from './components/AddTodo';
import axios from 'axios';

export default {
  name: 'App',

  components: {
    Header,
    Todos,
    AddTodo    
  },
  
  //"data" is a function that returns an object
  data() {
    return {
      msg: 'Hello', //Access in the template like "{{ msg }}"
      //'todos' is an array of objects
      todos: [ ]
    }
  },

  methods: {
    deleteTodo(id) {
      axios.delete(`http://127.0.0.1:8000/api/task-delete/${id}`)
        .then(this.todos = this.todos.filter(todo => todo.id != id))
        .catch(err => console.log(err))
      //'filter' is higher order array method for looping thorugh
      //just like 'for each' but conditions are applied using 'arrow' function
      
      //this.todos = this.todos.filter(todo => todo.id != id);
    },

    addTodo(newTodo) {
      const {title, completed} = newTodo;

      //When we make post request it gives back the item in "res.data" 
      //that we posted after saving it
      axios.post('http://127.0.0.1:8000/api/task-list/', {
        title,     //pulled from newTodo
        completed
      })
        //".then" is a promise
        .then(res => this.todos = [...this.todos, res.data])
        .catch(err => console.log(err));
      // '...' copies content [to this, from this]
     // this.todos = [...this.todos, newTodo];
    }

  },

  created(){
    axios.get('http://127.0.0.1:8000/api/task-list/')
      //filling up todos array with response.data
      .then(res => this.todos = res.data)
      .catch(err => console.log(err));
  }

}
</script>



<style>
  * {
    box-sizing: border-box;
    margin:0;
    padding:0;
  }

  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height:1.4;
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
