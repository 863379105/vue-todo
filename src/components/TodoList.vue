<template>
    <div id="todo-list">
        <input type="text" name="" id="" @keydown.enter="addList" v-model="inputContent">
        <ul>
            <li v-for="item in todoList" :key="item.id" :class="{'completed':item.status}">
                {{item.content}}
                <button class="delete-btn" @click="deleteTodo(item.id)">删除</button>
                <button class="complete-btn" @click="completeTodo(item.id)">完成</button>
            </li>
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
            console.log(newTodo);
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
                console.log('ok');
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
    .completed{
        text-decoration: line-through;
    }
    ul li{
        position: relative;
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