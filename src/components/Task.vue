<template>
<!--here we are toggling the true or false of each reminder, if task.reminder true then color output
 or else nothing,
at the same time added the task class again to make sure the class is always present-->
<div @dblclick="$emit('toggle-reminder', task.id)" :class="[task.reminder ? 'reminder' : '', 'task']"> 


<!--im implementing the custom events in two ways, one by declaring a methods object in script and the other 
    by directly inputting $emit in the template itself-->


    <h3>{{task.text}}
        <i @click="onDelete(task.id)"  class="fas fa-times"></i> </h3>
    <p1 >{{task.day}}</p1>
</div>
    
</template>

<script>
export default {
    name: 'Task',
    props: { 
        task: Object
},
    methods: {
        onDelete(id){
//this is a custom event where we want the delete task function to be used in the app.vue, so when we
//emit at first this is now accessible by the tasks.vue 
            this.$emit('delete-task', id) 

        }
    }
}

</script>

<style scoped>

.fas {
  color: red;
}
.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}
.task.reminder {
  border-left: 5px solid green;
}
.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

</style>