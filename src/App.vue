<script setup>
import { reactive } from 'vue';

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

        <header class="p-5 mb-4 mt-4 bg-light rounded-3">
            <h1>My Tasks</h1>
            <p>
                You have {{  getPendingTasks().length }} pending tasks
            </p>
        </header>
        <form @submit.prevent="registerTask">
            <div class="row">

                <div class="col">
                    <input  :value="state.tempTask" @change="event => state.tempTask = event.target.value" required type="text" placeholder="Insert the task description" class="form-control">
                </div>

                <div class="col-md-2">
                    <button class="btn btn-primary" type="submit">register</button>
                </div>

                <div class="col-md-2">
                    <select @change="event => state.filter = event.target.value" class="form-control">
                        <option value="all">All tasks</option>
                        <option value="pending">Pending</option>
                        <option value="acomplished">Acomplished</option>
                    </select>
                </div>

            </div >
        </form>
        <ul class="list-group mt-4">

            <li class="list-group-item" v-for="task in getFilteredTasks()">

                <input @change="event => task.acomplished = event.target.checked" :checked="task.acomplished" :id="task.title" type="checkbox">

                <label :class="{ done: task.acomplished}" class="ms-3" :for="task.title">
                    {{  task.title }}
                </label>
            </li>

        </ul>
    </div>
</template>

<style scoped>
.done{
    text-decoration: line-through;
}
</style>
