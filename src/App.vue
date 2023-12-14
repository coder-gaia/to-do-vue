<script setup>
    import { reactive } from 'vue';
    import   Head  from './components/Head.vue';
    import  Formulary  from './components/Formulary.vue';
    import  Todolist  from './components/Todolist.vue';

const state = reactive({
    filter: 'all',
    tempTask: '',
    tasks:[
        {
            title: 'Study Grunt',
            acomplished: false
        },
        {
            title: 'Study LESS',
            acomplished: false
        },
        {
            title: 'Go to the gym',
            acomplished: true
        }
    ]
})

const getPendingTasks = ()=>{
    return state.tasks.filter( task => !task.acomplished)
}
const getAcomplishedTasks = ()=>{
    return state.tasks.filter( task => task.acomplished)
}
const getFilteredTasks = ()=>{
    const { filter } = state

    switch(filter){
        case 'pending':
            return getPendingTasks();
        case 'acomplished':
            return getAcomplishedTasks();
        default:
            return state.tasks
    }
}
    const registerTask = () =>{
        const newTask = {
            title: state.tempTask,
            acomplished: false
        }
        state.tasks.push(newTask)
        state.tempTask = ''
    }

</script>

<template>
    <div class="container">
        <Head :pendingTasks="getPendingTasks().length" />
        <Formulary :changeFilter="ev => state.filter = ev.target.value" :tempTask="state.tempTask" :editTempTask="ev => state.tempTask = ev.target.value" :registerTask="registerTask"/>
        <Todolist :tasks="getFilteredTasks()"/>
    </div>
</template>


<style>
.label-done{
    text-decoration: line-through;
}
</style>
