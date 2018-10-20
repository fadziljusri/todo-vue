<template id="task-item">
    <li class="list-group-item d-flex justify-content-between align-items-center p-2" style="cursor: pointer">
      <span class="w-100 px-2 text-left" :class="className"
          @click.self="$emit('complete')"
      >
        {{ task.title }}
        <span v-if="task.completed" class="badge badge-success mx-2">completed</span>
      </span>
      <button class="btn btn-danger btn-sm"
              @click="$emit('remove')"
      >
        <!--<i class="fa fa-times"></i>-->
        Remove
      </button>
    </li>
</template>

<script>
export default {
  name: 'TaskItem',
  props: ['task'],
  computed: {
    className () {
      let classes = ['tasks__item__toggle']
      if (this.task.completed) {
        classes.push('tasks-completed')
      }
      return classes.join(' ')
    }
  }
}
</script>

<style scoped>
  .tasks-completed {
     text-decoration: line-through;
  }
</style>
