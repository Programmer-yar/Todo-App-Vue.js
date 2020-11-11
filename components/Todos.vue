<!-- 
- This part takes 'todos' array from parent "App.vue".
- It then loops through the array.
- During each iteration it calls its child "TodoItem" and passes 'todo.id'
- It also passes id of the item to be deleted to its parent "App.vue" 
 -->
<template>
	<div>
		<div v-bind:key="todo.id" v-for="todo in todos">
			<!-- <h3>{{ todo.title }}</h3> -->
			<!-- Again Up one order by using "$emit(name, value)" -->
			<!-- Will be catched in "App.vue" -->
			<TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo.id)"/>
		</div>
	</div>
</template>


<script>
import TodoItem from './TodoItem.vue';

export default {
	name: "Todos",
	components: {
		TodoItem
	},
	props: ["todos"] 
	//"props" contains properties/variables/data which are passed from parent to child
}
</script>



<style scoped>
	
</style>