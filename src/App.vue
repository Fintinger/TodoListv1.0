<template>
  <div class="todoContainer">
    <TodoHeader @receive2Add="receive2Add"/>
    <TodoList  :todos="todos"/>
    <TodoFooter :todos="todos" @checkAll="checkAll" @DelAll="DelAll"/>
  </div>
</template>

<script>
import TodoHeader from "@/components/TodoHeader";
import TodoList from "@/components/TodoList";
import TodoFooter from "@/components/TodoFooter";

export default {
  name: "App",
  components: {TodoHeader, TodoList, TodoFooter},
  data() {
    return {
      todos:JSON.parse(localStorage.getItem("todos")) || []
    }
  },
  methods: {
    //添加todo
    receive2Add(todoObj) {
      this.todos.unshift(todoObj)
    },
    //改变completed
    checkTodo(id) {
      this.todos.forEach(ele => {
        if (ele.id === id) ele.completed = !ele.completed
      })
    },
    //更新一个Todo
    updateTodo(id,val){
      this.todos.forEach(ele => {
        if (ele.id === id) ele.name = val
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
  },
  watch:{
    todos:{
      deep:true,
      handler(val){
        localStorage.setItem("todos",JSON.stringify(val))
      }
    }
  },
  mounted() {
    this.$bus.$on('checkTodo',this.checkTodo)
    this.$bus.$on('delTodo',this.delTodo)
    this.$bus.$on('updateTodo',this.updateTodo)
  },
  beforeDestroy() {
    this.$bus.$off('checkTodo')
    this.$bus.$off('delTodo')
    this.$bus.$off('updateTodo')
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
  color: #fff;
  padding: 5px;
  display: inline-block;
  box-sizing: border-box;
  cursor: pointer;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, .2), 0 1px 2px rgba(0, 0, 0, .05);
  border: none;
  border-radius: 3px;
  transition: all .1s;
  margin: 0;
}
button.btn_danger{
  background: #da4f49;
  border: 1px solid #d03329;
}
button.btn_danger:hover {
  background: #D03329FF;
}
button.btn_edit{
  background: #71ceed;
  border: 1px solid #61cbeb;
  margin-right: 5px;
}
button.btn_edit:hover {
  background: #46BCDFFF;
}
</style>