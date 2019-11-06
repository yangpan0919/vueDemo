<template>
  <ul class="todo-main">

   <ToDoItem v-for="(todo, index) in todos" :key="index" :todo="todo" :removeItem="removeItem" :index="index"/>
  </ul>
</template>

<script>
  import ToDoItem from './ToDoItem'
  export default {
    props: {
      todos: Array,
      removeItem: Function
    },
    data () {
      return {
        isShow: true
      }
    },
    components: {
      ToDoItem
    }
  }
</script>

<style scoped>

  /*main*/
  .todo-main {
    margin-left: 0px;
    border: 1px solid #ddd;
    border-radius: 2px;
    padding: 0px;
  }

  .todo-empty {
    height: 40px;
    line-height: 40px;
    border: 1px solid #ddd;
    border-radius: 2px;
    padding-left: 5px;
    margin-top: 10px;
  }

</style>
