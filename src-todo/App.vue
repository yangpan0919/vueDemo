<template>
  <div class="todo-container">
    <div class="todo-wrap">
      <ToDoHeader :addToDo="addToDo"/>
      <ToDoList :todos="todos" :removeItem="removeItem"/>
      <ToDoFooter :todos="todos" :selectAll="selectAll" :removeAllCompleted="removeAllCompleted"/>

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
    },
    data () {
      return {
        todos: JSON.parse(window.localStorage.getItem('todos-key') || '[]') //从本地获取存储数据
        // todos: [
        //   {title: '吃饭', complete: false},
        //   {title: '睡觉', complete: true},
        //   {title: '打豆豆', complete: false}
        // ]
      }
    },
    methods: {
      addToDo (todo) {
        this.todos.unshift(todo)
      },
      selectAll (flag) {
        this.todos.forEach(todo => {
          todo.complete = flag
        })
      },
      removeItem (index) {
        this.todos.splice(index, 1)
      },
      removeAllCompleted () {
        this.todos = this.todos.filter(todo => !todo.complete)
      }
    },
    watch: {
      todos: {
        deep: true,
        handler: function (value) {
          window.localStorage.setItem('todos-key', JSON.stringify(value))
        }

      }
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
