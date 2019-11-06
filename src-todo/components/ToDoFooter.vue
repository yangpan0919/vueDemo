<template>
  <div class="todo-footer">
    <label>
      <input :onclick="temptext" :class="bg" type="checkbox" v-model="allCheck"/>
    </label>
    <span>
          <span>已完成{{completed}}</span> / 全部{{todos.length}}
        </span>
    <button class="btn btn-danger" @click="delAllCompleted">清除已完成任务</button>
  </div>
</template>

<script>
  export default {
    props: {
      todos: Array,
      selectAll: Function,
      removeAllCompleted: Function
    },
    computed: {
      temptext () {
        return this.todos.length > 0 ? 'return true' : 'return false'
      },
      bg () {
        return this.todos.length > 0 ? 'tempc' : 'tempd'
      },
      completed () {
        return this.todos.reduce((previousValue, todo) => previousValue + (todo.complete ? 1 : 0), 0)
      },
      allCheck: {
        get () { // 是否勾选
          return this.completed === this.todos.length && this.todos.length > 0
        },
        set (newValue, oldValue) {
          this.selectAll(newValue)
        }
      }
    },
    methods: {
      delAllCompleted () {
        if (window.confirm('确定清除已完成的吗?')) {
          this.removeAllCompleted()
        }
      }
    }
  }
</script>

<style scoped>

  .tempc {
    background: red;
  }

  .tempd {
    background: black;
  }

  /*footer*/
  .todo-footer {
    height: 40px;
    line-height: 40px;
    padding-left: 6px;
    margin-top: 5px;
  }

  .todo-footer label {
    display: inline-block;
    margin-right: 20px;
    cursor: pointer;
  }

  .todo-footer label input {
    position: relative;
    top: -1px;
    vertical-align: middle;
    margin-right: 5px;
  }

  .todo-footer button {
    float: right;
    margin-top: 5px;
  }
</style>
