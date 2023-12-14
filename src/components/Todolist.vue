<script setup>
const { tasks } = defineProps(['tasks']);
</script>

<template>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="task in tasks">
            <input @change="event => task.acomplished = event.target.checked" :checked="task.acomplished" :id="task.title"
                type="checkbox">
            <label :class="{ 'label-done': task.acomplished }" class="ms-3" :for="task.title">
                {{ task.title }}
            </label>

        </li>
    </ul>
</template>
