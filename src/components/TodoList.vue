<template>
    <div id="todo-list">
        <input type="text" name="" id="" @keydown.enter="addList" v-model="inputContent">
        <ul>
            <li v-for="item in todoList" :key="item.id">{{item}}</li>
        </ul>
    </div>
</template>

<script>
export default {
    name : 'TodoList',
    data() {
        return {
            inputContent : '',
            todoList : [{
                id : 1,
                content : '123',
            },{
                id : 2,
                content : '123',
            }]
        }
    },
    methods : {
        addList(){
            let newTodo = {
                id : this.getTodoId(),
                content : this.inputContent
            }
            console.log(newTodo);
            this.todoList.push(newTodo)
        },
        getTodoId(){
            let year = new Date().getFullYear().toString()
            let month = (new Date().getMonth() + 1).toString()
            let day = new Date().getDate().toString()
            let hour = new Date().getHours().toString()
            let minute  = new Date().getMinutes().toString()
            let second = new Date().getSeconds().toString()
            let num = Math.ceil(Math.random() * 100000).toString()
            return (year + month + day + hour + minute + second + num)
        }
    }
}
</script>

<style scoped>
    input{
        display: block;
        margin: 0 auto;
    }
    #todo-list{
        width: 40%;
        margin: 100px auto;
        border: 1px tomato solid;
        padding: 5px;
    }
</style>