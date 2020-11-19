<template>
    <div id="todo-list">
        <input type="text" name="" id="" @keydown.enter="addList" v-model="inputContent">
        <ul>
            <todo-item 
                v-for="todo in todoList" 
                :key="todo.id" 
                :todo = 'todo' 
                @deleteTodo='deleteTodo' 
                @completeTodo='completeTodo'>
            </todo-item>
        </ul>
    </div>
</template>

<script>
import TodoItem from './TodoItem'
export default {
    name : 'TodoList',
    components:{
        TodoItem
    },
    data() {
        return {
            inputContent : '',
            todoList : [{
                id : 1,
                content : '123',
                status : false,
            },{
                id : 2,
                content : '123',
                status : true
            }],
        }
    },
    methods : {
        addList(){
            let newTodo = {
                id : this.getTodoId(),
                content : this.inputContent,
                status : false
            }
            this.todoList.push(newTodo)
            this.inputContent = ''
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
        },
        deleteTodo(id){

            this.todoList = this.todoList.filter((item) => {
                return item.id !== id
            })
        },
        completeTodo(id){
            this.todoList.forEach((item) => {
                if(item.id === id){
                    item.status = !item.status
                }
            })
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
    
    ul li{
        position: relative;
    }
    
</style>