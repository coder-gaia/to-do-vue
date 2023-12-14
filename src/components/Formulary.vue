<script setup>
    const { tempTask, editTempTask, registerTask, changeFilter } = defineProps(['tempTask', 'editTempTask', 'registerTask', 'changeFilter']);
</script>

<template>
    <form @submit.prevent="registerTask">
        <div class="row">
            <div class="col">
                <input  :value="tempTask" @change="editTempTask" required type="text" placeholder="Insert the task description" class="form-control">
            </div>
            <div class="col-md-2">
                <button class="btn btn-primary" type="submit">register</button>
            </div>
            <div class="col-md-2">
                <select @change="changeFilter" class="form-control">
                    <option value="all">All tasks</option>
                    <option value="pending">Pending</option>
                    <option value="acomplished">Accomplished</option>
                </select>
            </div>
        </div>
    </form>
</template>
