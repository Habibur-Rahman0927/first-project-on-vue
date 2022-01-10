<template>
  <section>
  <Header title="Task Tracker" @toggle-add="toggleAddTask" :showAddTask="showAddTask" />
  <div v-show="showAddTask">
    <AddTask @add-task="addTask"/>
  </div>
  <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" v-bind:tasks="tasks" />
  </section>
</template>

<script>
import Header from './components/Header';
import Tasks from './components/Tasks';
import AddTask from './components/AddTasks';
export default {

  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask
  },
  data(){
    return {
      tasks: [],
      showAddTask: false
    }
  },
  methods:{
    addTask(task){
      this.tasks = [...this.tasks, task];
    },
    deleteTask(id){
      if(confirm('Are you sure?')){
        this.tasks = this.tasks.filter((task) => task.id !== id)
      }
    },
    toggleReminder(id){
      this.tasks = this.tasks.map((task) => task.id === id ? {...task, reminder: !task.reminder}: task)
    },
    toggleAddTask(){
      this.showAddTask = !this.showAddTask
    },
    async fetchTasks(){
      const res = await fetch('http://localhost:5000/api/tasks/')
      const data = await res.json();
      return data;
    },
  },
  async created(){
    this.tasks = await this.fetchTasks()
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
