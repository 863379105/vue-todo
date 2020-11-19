<template>
    <div class="wrapper clear-fix">
        <div class="confirm-btn" @click="completeTodo(todo.id)">
            <i class="iconfont icon-dui" :class="{'element-dis': !todo.status}"></i>
        </div>
        <li :class="{'completed':todo.status}">
            {{todo.content}}
        </li>
        <div class="delete-btn" @click="deleteTodo(todo.id)"><i class="iconfont icon-cuo"></i></div>
    </div>
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
    .clear-fix:after{
        content: '';
        height: 0;
        display: block;
        clear: both;
    }
    .element-dis{
        display: none;
    }
    .completed{
        text-decoration: line-through;
    }
    .wrapper{
        position: relative;
        box-shadow: 1px 1px 5px	#B0B0B0;
    }
    li{
        list-style: none;
        display: block;
        width: 90%;
        height: 50px;
        line-height: 50px;
        font-size: 18px;
        float: right;
        margin-right: 20px;
        color: #555555;
        font-weight: lighter;
    }
    .confirm-btn{
        height: 25px;
        width: 25px;
        border-radius: 100%;
        position: absolute;
        left: 20px;
        top: 50%;
        transform: translateY(-50%);
        border: 1px #B0B0B0 solid;
        cursor: pointer;
    }
    .confirm-btn i{
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%,-50%)
    }
    .delete-btn{
        height: 20px;
        width: 20px;
        position: absolute;
        right: 20px;
        top: 50%;
        transform: translateY(-50%);
        cursor: pointer;
    }
    .delete-btn i{
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%,-50%)
    }
</style>