<script>
  import Task from './components/Task.vue';
  import AddTask from './components/AddTask.vue';
  import Tabs from './components/Tabs.vue';

  export default {
    components: { Task, AddTask, Tabs },
    data() {
      return {
        inputTask: '',
        error: '',
        tasks: [],
        selectTask: 0
      };
    },
    computed: {
      filteredTasks() {
        switch (this.selectTask) {
          case 0:
            return this.tasks; // Показываем все задачи
          case 1:
            return this.tasks.filter((task) => !task.status); // Только активные задачи
          case 2:
            return this.tasks.filter((task) => task.status); // Только завершенные задачи
          default:
            return [];
        }
      }
    },
    methods: {
      changeInput(val) {
        this.inputTask = val;
      },
      addTask() {
        if (this.inputTask.length > 50) {
          this.error = 'Слишком большой текст';
          return;
        } else if (this.inputTask.length < 2) {
          this.error = 'Введите хотя бы пару символов';
          return;
        } else {
          this.error = '';
        }

        let uniqueId = Date.now().toString() + Math.random().toString(36).substr(2, 9);

        this.tasks.push({ id: uniqueId, text: this.inputTask, status: false });
        localStorage.setItem('tasks', JSON.stringify(this.tasks));
        this.inputTask = '';
      },
      deleteTask(id) {
        this.tasks = this.tasks.filter(task => task.id !== id)
        localStorage.setItem('tasks', JSON.stringify(this.tasks));
        console.log(`Удаление задачи с индексом ${id}`)
        
      },

      setStatus(id, value) {
        const task = this.tasks.find(task => task.id === id);
        if (task) {
          task.status = value;
          localStorage.setItem('tasks', JSON.stringify(this.tasks));
        }
        console.log(this.tasks)
      },

      selectStatus(value) {
        this.selectTask = value;
      }
    },
    mounted() {
      const saved = localStorage.getItem('tasks');
      if (saved) {
        this.tasks = JSON.parse(saved);
        console.log("Загружено из localStorage:", this.tasks);
      } else {
        console.log("Задачи не найдены в localStorage");
      }
    }
  };
</script>

<template>
  <h1>Task Book</h1>
  <AddTask :changeInput="changeInput" :addTask="addTask" />
  <p v-show="error != ''">{{ error }}</p><br /><br />
  <Tabs :selectStatus="selectStatus" :selectTask="selectTask" />

  <Task v-for="(el) in filteredTasks" :key="el.id" :text="el.text" :deleteTask="deleteTask"
    :setStatus="setStatus" :status="el.status" :selectTask="selectTask" :id="el.id" />
</template>

<style scoped></style>