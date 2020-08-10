<template>
  <div>
   <router-link to="/">
     Go to Home
   </router-link>
    <AddTodo
      @add-todo-item="addTodo"
    />
    <select v-model="filter">
      <option value="all">
        All
      </option>
      <option value="completed">
       Completed
      </option>
      <option value="not-completed">
        Not Completed
      </option>
    </select>
    <hr>
    <Loader v-if="loading"/>
    <TodoList
      v-else-if="todo_list.length"
      v-bind:todo_list="filteredTodos"
      @remove-todo="removeTodo"/>

  <p v-else>
    No todos!
  </p>
  </div>
</template>
<script>
  import TodoList from "./../components/TodoList";
  import AddTodo from "./../components/AddTodo";
  import Loader from "./../components/Loader";

  export default {
    data(){
      return {
        todo_list: [],
        loading:true,
        filter:'all'
      }
    },
    mounted(){
      const url = 'https://jsonplaceholder.typicode.com/todos?_limit=3'; // get data from  api componentdidmount()
      fetch(url)
        .then(response => response.json())
        .then(json => {
          setTimeout(()=> {
            this.todo_list = json;
            this.loading = false;
          },1000)

        })
    },

    computed:{

    filteredTodos() { // переменная
      if (this.filter ==='all') {
        return this.todo_list
      }

      if (this.filter ==='completed') {
        return this.todo_list.filter(t=> t.completed)
      }
      if (this.filter ==='not-completed') {
        return this.todo_list.filter(t=> !t.completed)
      }
    }
      },

    methods: {
      removeTodo(id) {
        this.todo_list = this.todo_list.filter(t => t.id !== id)
      },
      addTodo(todo) {
        this.todo_list = [...this.todo_list, todo];
      }
    },

    components: {
      TodoList,
      AddTodo,
      Loader
    }
  }
</script>
