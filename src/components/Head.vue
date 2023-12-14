<script setup>
    const props = defineProps(['pendingTasks'])
</script>

<template>
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
        <h1>My Tasks</h1>
        <p v-if="props.pendingTasks > 0">
            You have {{ props.pendingTasks }} pending tasks
        </p>
        <p v-else-if="props.pendingTasks <= 0">
            You don't have pending tasks
        </p>
    </header>
</template>