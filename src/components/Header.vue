<template>
    <header>
        <h1>
            {{title}}
        </h1>
        <!--if add task is true then green or else red-->
<Button @btn-click="$emit('toggle-add-task')"
 :text="showAddTask ? 'Close' : 'Add Task'"
 :color="showAddTask ? 'red' : 'green'" />
    </header>
</template>

<script>

import Button from './Button.vue' 

    export default{
        name: 'Header',
        //props are registered here to be used in the template
        props: {
            title: String,
            showAddTask: Boolean
        },

        components:{
            Button
        }


        
    }
</script>

<style scoped>
header{
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
}
</style>