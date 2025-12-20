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

      this.tasks.push({ text: this.inputTask, status: false });
      localStorage.setItem('tasks', JSON.stringify(this.tasks));
      this.inputTask = '';
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
      localStorage.setItem('tasks', JSON.stringify(this.tasks));
      this.$forceUpdate();
      location.reload(); // Вероятно, лучше убрать reload(), поскольку forceUpdate() достаточно
    },
    setStatus(index, value) {
      this.tasks[index].status = !this.tasks[index].status;
      localStorage.setItem('tasks', JSON.stringify(this.tasks));
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
  <Tabs :selectStatus="selectStatus" />

  <!-- Используем вычисляемое свойство для фильтрации задач -->
  <Task
    v-for="(el, index) in filteredTasks"
    :key="index"
    :text="el.text"
    :deleteTask="deleteTask"
    :index="index"
    :setStatus="setStatus"
    :status="el.status"
    :selectTask="selectTask"
  />
</template>

<style scoped></style>