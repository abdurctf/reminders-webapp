<template>
    <div :key="task.id" v-for="task in tasks" > <!--this is how we loop thru the array of data we wanted to enter-->
    <Task @toggle-reminder="$emit('toggle-reminder', task.id)"
     @delete-task="$emit('delete-task', task.id)" :task="task" />
<!--checking if the parameter of the custom event has to be id or task.id-->

    </div>
</template>

<script>
import Task from './Task'

export default {
    name: 'Tasks',
    props: {
        tasks: Array
    },

    components: {//registering the components over here
        Task
    },

    emits: ['delete-task', 'toggle-reminder']
        
    }

</script>