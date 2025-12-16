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
      },
      addTask() {
        if (this.inputTask.length > 50) {
          this.error = 'Слишком большой текст'
          return
        }
        else if (this.inputTask.length <2) {
          this.error = 'Введите хотя бы пару символов'
          return
        }
        else {
          this.error = ''
        }
      }
    }
  }
</script>

<template>
  <h1>Task Book</h1>
  <AddTask :changeInput="changeInput" :addTask="addTask"/>
  <p v-show="error != ''">{{error}}</p>
  <Task />
  <Task />
</template>

<style scoped>

</style>