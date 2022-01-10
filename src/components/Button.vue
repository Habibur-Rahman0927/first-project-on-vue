<template>
    <div>
        <button @click="onclick()" :style="{background: color, color: 'white'}" class="btn">{{text}}</button>
    </div>
</template>

<script>
export default {
    name: 'Button',
    props:{
        text:{
            type:String,
            default: 'Add Task',    
        },
        color:{
            type: String,
            default: 'green',
        }
    },
    methods:{
        onclick(){
            this.$emit('toggle-add')    
        }
    }
}
</script>