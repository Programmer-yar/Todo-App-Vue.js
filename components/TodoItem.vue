<!-- 
- This is child of "Todos.vue".
- It gets 'todo' item of 'todos' array from its parent "Todos.vue"
- This part creates a div containing 'checkbox' with 'item title' and 
  'delete' button 
- It also passes id of the item to be deleted to its parent -->

<template>
  <!-- v-bind attaches conditional class "{'class_name':condition}" -->
	<div class="todo-item" v-bind:class="{'is-complete':todo.completed}">
		<p>
      <!-- "v-on" is used to add event -->
      <input type="checkbox" v-on:change="markComplete">
      {{ todo.title }}
      <!-- we can also use 'v-on' in place of '@click' -->
      <!-- Up one order by using "$emit(name, value)" -->
      <button @click="$emit('del-todo', todo.id)" class="del">X</button>
    </p>		
	</div>
</template>


<script>
export default {
	name: "TodoItem",
	props: ["todo"],  //'Props' means properties
  //props are used to pass data from parent down to child component
  methods:{
    markComplete() {
      this.todo.completed = !this.todo.completed;
    }
  }
}
</script>



<style scoped>
	.todo-item {
    background: #f4f4f4;
    padding: 10px;
    border-bottom: 1px #ccc dotted;
  }

  .is-complete {
    text-decoration: line-through;
  }

  .del {
    background: #ff0000;
    color: #fff;
    border: none;
    padding: 5px 9px;
    border-radius: 50%;
    cursor: pointer;
    float: right;
  }
</style>