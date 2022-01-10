<template>
    <header class="container">
        <h1>{{title}}</h1>
        <Button @toggle-add="$emit('toggle-add')" :text="showAddTask ? 'close':'Add Task'" :color="showAddTask ? 'red': 'green'" />
    </header>
</template>

<script>
import Button from './Button.vue';
export default {
    name: 'Header',
    props:{
        title:{
            type: String,
            default: 'Hello Task'
        },
        showAddTask:Boolean,
    },
    components:{
        Button
    }
}
</script>

<style scoped>
    header{
        display:flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 20px;
    }
</style>