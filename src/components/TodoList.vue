<template>
    <div id="todo-list">
        <div class="todo-title">todos</div>
        <header>
            <div class="confirm-btn" @click="allcheck" :class="{'element-dis':!todoList.length}">
                <i class="iconfont icon-dui" :class="{'element-dis':!allChecked}"></i>
            </div>
            <input type="text" name="" id="" 
                maxlength="30"
                v-on:keydown.enter="addList" 
                v-model="inputContent" 
                @focus = "clearMsg" 
                @blur="showMsg" 
                :class="{'default-msg':isDefaultMsg}">
        </header>
        <article :class="'clear-fix'">
            <todo-item 
                v-for="todo in todoList" 
                :key="todo.id" 
                :todo = 'todo' 
                @deleteTodo='deleteTodo' 
                @completeTodo='completeTodo'>
            </todo-item>
        </article>
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
            inputContent : 'What need to be done?',
            todoList : [],
            allChecked : false,
            isDefaultMsg : true
        }
    },
    methods : {
        addList(){
            if(this.inputContent === ''){
                return
            }
            let newTodo = {
                id : this.getTodoId(),
                content : this.inputContent,
                status : false
            }
            
            this.todoList.push(newTodo)
            this.inputContent = ''
            this.allChecked = this.todoList.every((item)  => {
                return item.status
            })
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
            this.allChecked = this.todoList.every((item)  => {
                return item.status
            })
        },
        completeTodo(id){       
            this.todoList.forEach((item) => {
                if(item.id === id){
                    item.status = !item.status
                }
            })
            this.allChecked = this.todoList.every((item)  => {
                return item.status
            })
        },
        allcheck(){
            console.log('ok');
            this.todoList.forEach((item) => {
                item.status = !this.allChecked
            })
            this.allChecked = !this.allChecked
        },
        clearMsg(){
            if(this.inputContent === 'What need to be done?'){
                this.inputContent = '',
                this.isDefaultMsg = false
            }
        },
        showMsg(){
            if(this.inputContent === ''){
                this.inputContent = 'What need to be done?'
                this.isDefaultMsg = true
            }
            
        }
    }
}
</script>

<style scoped>

    .todo-title{
        text-align: center;
        font-size: 100px;
        font-weight: lighter;
        color: rgb(233,213,213);
        background-color: rgb(244, 244, 244);
    }
    .default-msg{
        font-style: italic;
        color: #dadada;
        font-weight: lighter;
    }
    .element-dis{
        display: none;
    }
    .clear-fix:after{
        content: '';
        height: 0;
        display: block;
        clear: both;
    }
    #todo-list{
        width: 60%;
        margin: 30px auto;
        position: relative;
        background-color: rgb(255, 255, 255);
    }
    header{
        box-shadow: 1px 1px 5px	#B0B0B0;
        /* overflow: hidden; */
        position: relative;
        height: 50px;
    }
    input{
        border:none;
        outline: none;
        display: block;
        width: 90%;
        position: absolute;
        right: 20px;
        top:50%;
        transform:translateY(-50%);
        height: 50px;
        line-height: 50px;
        font-size: 18px;
        color: #B0B0B0;
    }
    article{
        position: relative;
    }
    .confirm-btn{
        height: 25px;
        width: 25px;
        border-radius: 100%;
        position: absolute;
        left: 20px;
        top: 50%;
        transform: translateY(-50%);
        border: 1px	#B0B0B0 solid;
        cursor: pointer;
    }
    .confirm-btn i{
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%,-50%)
    }
</style>