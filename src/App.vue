<template>
  <div id="app">
    <img src="./assets/logo.png">
    <router-view/>
    <task-list :tasks="todos" @clear:completed="clearCompleted()" @clear:all="todos = []"></task-list>
  </div>
</template>

<script>
import 'bootstrap/dist/css/bootstrap.css'
import TaskList from './components/TaskList'

export default {
  name: 'App',
  components: {
    TaskList
  },
  data () {
    return {
      todos: [
        {title: 'Learn Vue', completed: true},
        {title: 'Learn Vuex', completed: false}
      ]
    }
  },
  methods: {
    clearCompleted () {
      this.todos = this.todos.filter(this.inProgress)
    },
    inProgress (task) {
      return !this.isCompleted(task)
    },
    isCompleted (task) {
      return task.completed
    }
  }
}
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
