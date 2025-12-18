<script>
  import Task from './components/Task.vue'
  import AddTask from './components/AddTask.vue'

  export default {
    components: { Task, AddTask },
    data() {
      return {
        inputTask: '',
        error: '',
        tasks: []
      }
    },
    mounted() {
      const saved = localStorage.getItem('tasks')
      if (saved) {
        this.tasks = JSON.parse(saved)
        console.log("Загружено из localStorage:", this.tasks)
      } else {
        console.log("Задачи не найдены в localStorage")
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
        else if (this.inputTask.length < 2) {
          this.error = 'Введите хотя бы пару символов'
          return
        }
        else {
          this.error = ''
        }

        this.tasks.push({
          text: this.inputTask,
          status: false
        })
        localStorage.setItem('tasks', JSON.stringify(this.tasks));
        this.inputTask = ''
      },
      deleteTask(index) {
        this.tasks.splice(index, 1)
        localStorage.setItem('tasks', JSON.stringify(this.tasks));
        this.$forceUpdate()
        location.reload()
      },
      setStatus(index, value) {
        this.tasks[index].status = !this.tasks[index].status
        localStorage.setItem('tasks', JSON.stringify(this.tasks));
      }
    }
  }
</script>

<template>
  <h1>Task Book</h1>
  <AddTask :changeInput="changeInput" :addTask="addTask" />
  <p v-show="error != ''">{{error}}</p><br><br>
  <Task v-for="(el, index) in tasks" :key="index" :text="el.text" :deleteTask="deleteTask" :index="index" :setStatus="setStatus" :status="this.tasks[index].status" />
</template>

<style scoped>

</style>