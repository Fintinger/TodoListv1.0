<template>
  <div class="todoContainer">
    <TodoHeader :receive2Add="receive2Add"/>
    <TodoList :checkTodo="checkTodo" :todos="todos" :delTodo="delTodo"/>
    <TodoFooter :todos="todos" :checkAll="checkAll" :DelAll="DelAll"/>
  </div>
</template>

<script>
import TodoHeader from "@/components/TodoHeader";
import TodoList from "@/components/TodoList";
import TodoFooter from "@/components/TodoFooter";
import {nanoid} from "nanoid";

export default {
  name: "App",
  components: {TodoHeader, TodoList, TodoFooter},
  data() {
    return {
      todos: [
        {id: nanoid(), name: "学习vue.js", completed: true},
        {id: nanoid(), name: "学习javascript", completed: false},
        {id: nanoid(), name: "吃饭", completed: false},
      ]
    }
  },
  methods: {
    //添加todo
    receive2Add(todoObj) {
      this.todos.unshift(todoObj)
    },
    //改变completed
    checkTodo(id) {
      console.log(id);
      this.todos.forEach(ele => {
        if (ele.id === id) ele.completed = !ele.completed
      })
    },
    //删除一个todo
    delTodo(id){
      this.todos=this.todos.filter(el=>el.id!==id)
    },
    //全选或取消全选
    checkAll(val){
      this.todos.forEach(el=>el.completed=val)
    },
    //删除所有已经完成的项目
    DelAll(){
      this.todos=this.todos.filter(el=>el.completed!==true)
    }
  }
}
</script>

<style>
* {
  bottom: 0;
  padding: 0;
}

ul, li {
  text-decoration: none;
  list-style: none;
}

input {
  outline: none;
}

body {
  background: #fff;
  font-size: 14px;
}

.todoContainer {
  width: 500px;
  max-width: 90%;
  height: auto;
  margin: 0 auto;
  border: 2px solid #bcbcbc;
  padding: 10px;
  box-sizing: border-box;
  background: #ededed;

  border-radius: 5px;
}

.todoContainer > div {
  width: 100%;
}

button {
  background: #e55945;
  border: none;
  border-radius: 5px;
  color: #fff;
  padding: 5px;
  display: inline-block;
  box-sizing: border-box;
  cursor: pointer;
  margin-bottom: 0;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, .2), 0 1px 2px rgba(0, 0, 0, .05);

  transition: all .2s;
}

button:hover {
  background: #d55945;
}
</style>
