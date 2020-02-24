<template>
<form @submit.prevent="$emit('addNewTask')">
    <input type="text">
    <button type="submit"></button>
</form>
</template>

<script>
export default {
    props: {
        taskName: {
            type: String,
            required: true,
        }
    }
}
</script>