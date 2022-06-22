<template>
<div class="container">
  <Header  @toggle-add-task="toggleAddTask" title="Reminders" :showAddTask="showAddTask"/>

<!--checking if v-if or v-show yields the same result or not-->
<div v-if="showAddTask"> <AddTask @add-task="addTask"/>
  </div>

  

  <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />

<!--we are v-binding here since the tasks are stored in an array and is dynamically
 updated after each looping thru
  <Tasks :tasks="tasks" /> -->
</div>
  
</template>

<script>

import Header from './components/Header'
import Tasks from './components/Tasks'
import AddTask from './components/AddTask'


export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask
},

  data(){
    return{
      tasks: [],
      showAddTask: false
    }
  },

  methods: {
    deleteTask(id) {
      //we dont wanna directly delete tasks, so we are using filter
      //filter is an high order array method
      //here it means that we will iterate thru the array of tasks IF they are
      //not equal to the id, if they are, then deleteTask 
      if(confirm('Are you sure?')){
      this.tasks = this.tasks.filter((task) => task.id !== id)
      }
    },

    toggleReminder(id){
      /*We are mapping thru the entire array so for each task we want to check if the task.id is equal to
      the that's being passed in, if it is then we want to return an array of objects where we have the 
      initial task properties so we can spread across the initial task, so we want to change the reminder to
      the opposite of the current state of the reminder, else just return the original task
       */
      this.tasks = this.tasks.map((task) => task.id===id ? { ...task, reminder: !task.reminder}:task)
    },

    addTask(task){
      this.tasks = [...this.tasks, task]
    },

    toggleAddTask(){
      this.showAddTask = !this.showAddTask
    }

  },

  created(){
    this.tasks = [
      {
      id: 1,
      text: 'Learn Vue.js',
      day: 'June 9th at 12:27pm',
      reminder: true, 
    
  },
  {
    id: 2,
      text: 'Prepare for Coding Interview',
      day: 'June 9th at 12:27pm',
      reminder: true, 
  },
  {
    id: 3,
    text: 'Master C++',
    day: 'June 9th at 12:27pm',
    reminder: false
  }


]
  }
  
}
</script>


<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>

