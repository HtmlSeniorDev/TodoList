<template>
  <form @submit.prevent="onSubmit">
    <input type="text" v-model="title"/>
    <button type="submit">
      Create Todo
    </button>
  </form>
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
      onSubmit() {
        if (this.title.trim()) {
          const newTodo = {
            id: Date.now(),
            title: this.title,
            completed: false,
          };
          console.log(newTodo);
          this.$emit('add-todo-item', newTodo);
          this.title = ""
        }

      }
    }
  }
</script>

<style scoped>
  form {
    display: flex;
    margin-bottom: 20px;
    margin-top: 20px;
  }

  input {
    width:100%;
  }
</style>
