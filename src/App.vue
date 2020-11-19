<template>
  <div>
    <todo-list></todo-list>
  </div>
</template>

<script>
  import TodoList from "./components/TodoList.vue";

  export default {
    name: "App",
    components: {
      TodoList
    }
  };
</script>

<style>
@import "./assets/css/icon.css";
*{
  padding: 0;
  margin: 0;
}
body{
  background-color: rgb(244, 244, 244);
  font-family: 'Microsoft YaHei'
}
</style>
