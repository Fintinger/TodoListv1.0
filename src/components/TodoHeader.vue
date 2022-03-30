<template>
  <div class="todoHeader">
    <input v-model="title" placeholder="请输入你的任务名称,按回车键确认" type="text" @keyup.enter="addTodo">
  </div>
</template>

<script>
import {nanoid} from "nanoid"

export default {
  name: "TodoHeader",
  data() {
    return {
      title: ""
    }
  },
  methods: {
    addTodo() {
      //数据筛查
      if (!this.title.trim()) return alert("内容不能为空");
      //构建新数据
      const todoObj = {id: nanoid(), name: this.title, completed: false}
      //调用数据传输方法
      // this.receive2Add(todoObj);
      this.$emit("receive2Add",todoObj)
      //清空输入框
      this.title="";
    }
  }
}
</script>

<style scoped>
.todoHeader {
  overflow: hidden;
}

.todoHeader > input {
  width: 100%;
  height: 30px;
  padding: 0 10px;
  border: 1px solid #ececec;
  border-radius: 5px;
  box-sizing: border-box;

}

</style>