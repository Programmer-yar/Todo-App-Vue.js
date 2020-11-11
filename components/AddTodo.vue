<!-- 
- This part shows input form.
- It creates new object when input is given 
  and passes it to parent file "App.vue" using 'emit' method -->
<template>
  <div>
    <form @submit="addTodo">
      <input type="text" v-model="title" name="title" placeholder="Add Todo ...">
      <input type="submit" value="Submit" class="btn">
    </form>
  </div>
</template>


<script>

export default {
	name: "AddTodo",
  data() {
    return {
      title: '',

    }
  },

  methods: {
    addTodo(e) {
      e.preventDefault();
      //'const' = contruct, new object 'Todo'
      const newTodo = {
        //id: uuidv4(),
        title: this.title,
        completed: false
      }
      //send up to parent
      this.$emit('add-todo', newTodo);

      //Clears out the form after creating an object
      this.title = '';
    }
  }
}
</script>


<style scoped>
  form {
    display: flex;
  }

  input[type="text"] {
    flex: 10;
    padding: 5px;
  }

  input[type="submit"] {
    flex: 2;
  }

</style>