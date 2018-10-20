<template id="task-list">
  <section class="tasks">
    <h1 class="text-success">
      Tasks
      <transition name="fade">
        <small v-if="incomplete">({{ incomplete }})</small>
      </transition>

    </h1>
    <div class="input-group">
      <input type="text"
             class="form-control"
             v-model="newTask"
             @keyup.enter="addTask"
             placeholder="New task"
      >
      <div class="input-group-append">
          <button @click="addTask"
                  class="btn btn-outline-success"
          >
            <i class="fa fa-plus"></i> Add
          </button>
      </div>
    </div>

    <div class="btn btn-group px-0">
      <button type="button" class="btn btn-warning"
              @click="$emit('clear:completed')"
      >
        <i class="fa fa-check"></i> Clear Completed
      </button>
      <button class="btn btn-danger"
              @click="$emit('clear:all')"
      >
        <i class="fa fa-trash"></i> Clear All
      </button>
    </div>

    <transition-group name="fade" tag="ul" class="list-group">
      <task-item v-for="(task, index) in tasks"
                 @remove="removeTask(index)"
                 @complete="completeTask(task)"
                 :task="task"
                 :key="index"
      ></task-item>
    </transition-group>
  </section>
</template>

<script>
import TaskItem from './TaskItem'

export default {
  name: 'TaskList',
  components: {
    TaskItem
  },
  props: {
    tasks: {default: []}
  },
  data () {
    return {
      newTask: ''
    }
  },
  computed: {
    incomplete () {
      return this.tasks.filter(this.inProgress).length
    }
  },
  methods: {
    addTask () {
      if (this.newTask) {
        this.tasks.push({
          title: this.newTask,
          completed: false
        })
        this.newTask = ''
      }
    },
    completeTask (task) {
      task.completed = !task.completed
    },
    removeTask (index) {
      this.tasks.splice(index, 1)
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

<style scoped>
  .tasks {
    width: 100%;
    max-width: 45rem;
    padding: 1em;
    margin: 1em auto;
    overflow: auto;
    background-color: white;
    /*box-shadow:0px .25rem 1rem rgba(black, .25);*/
  }
</style>
