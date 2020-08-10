<template>
 <div>
   <ul>
     <TodoItem
       v-on:remove-todo="removeTodo"
       v-for="(todo,i) of todo_list"
       v-bind:todo="todo"
       v-bind:index="i"
       :key="todo.id"
      />
   </ul>
 </div>
</template>
<script>
    import TodoItem from "./TodoItem";
    export default {
      props:['todo_list'],
      components: {
          TodoItem
      },
      methods:{
        removeTodo(id){
          this.$emit('remove-todo',id)
        }
      }
    }
</script>

<style scoped>
  ul {
    list-style: none;
    margin: 0;
    padding: 0;
  }
</style>
