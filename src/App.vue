<template>
  <div class="todo-container">
    <div class="todo-wrap">
      <ToDoHeader/>
      <ToDoList/>
      <ToDoFooter/>

    </div>
  </div>
</template>

<script>
  import ToDoHeader from './components/ToDoHeader'
  import ToDoFooter from './components/ToDoFooter'
  import ToDoList from './components/ToDoList'

  export default {
    name: 'App',
    components: {
      ToDoFooter,
      ToDoHeader,
      ToDoList
    }
  }
</script>

<style scoped>

  /*app*/
  .todo-container {
    width: 600px;
    margin: 0 auto;
  }

  .todo-container .todo-wrap {
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
  }

</style>
