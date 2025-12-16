<script>
  import Task from './components/Task.vue'
  import AddTask from './components/AddTask.vue'

  export default {
    components: { Task, AddTask },
    data() {
      return {
        inputTask: '',
        error: ''
      }
    },
    methods: {
      changeInput(val) {
        this.inputTask = val
      }
    }
  }
</script>

<template>
  <h1>Task Book</h1>
  <AddTask :changeInput="changeInput"/>
  <p>{{inputTask}}</p>
  <Task />
  <Task />
</template>

<style scoped>

</style>