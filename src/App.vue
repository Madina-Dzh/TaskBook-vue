<script>
import Task from './components/Task.vue'
import AddTask from './components/AddTask.vue'

export default {
  components: {Task, AddTask},
  data() {
    return {
      // Объекты переменные
    }
  }
}
</script>

<template>
  <h1>Task Book</h1>
  <AddTask/>
  <Task/>
  <Task/>
</template>

<style scoped>
  
</style>
