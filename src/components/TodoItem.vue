<template>
    <li :class="{'completed':todo.status}">
        {{todo.content}}
        <button class="delete-btn" @click="deleteTodo(todo.id)">删除</button>
        <button class="complete-btn" @click="completeTodo(todo.id)">完成</button>
    </li>
</template>
<script>
    export default {
        name : 'TodeItem',
        props : ['todo'],
        methods : {
            deleteTodo(id){
                this.$emit('deleteTodo',id)
            },
            completeTodo(id){
            
               this.$emit('completeTodo',id)
            },
            
        }
    }
</script>
<style  scoped>
    .completed{
        text-decoration: line-through;
    }
    .delete-btn{
        position: absolute;
        right: 0;
    }
    .complete-btn{
        position: absolute;
        right: 50px 
    }
</style>