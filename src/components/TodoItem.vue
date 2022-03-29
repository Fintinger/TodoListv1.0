<template>
  <div class="itemWrapper ">
    <li>
      <label>
        <input :checked="todo.completed" type="checkbox" @change="handleCheck(todo.id)">
        <span>{{ todo.name }}</span>
      </label>
      <button @click="handleDelete(todo.id)">删除</button>
    </li>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo", "checkTodo", "delTodo"],
  methods: {
    handleCheck(id) {
      //通知App组件改变对应todo的completed值
      this.checkTodo(id)
    },
    handleDelete(id) {
      //通知App组件删除对应todo项
      if (confirm("是否删除该项？")) {
        this.delTodo(id)
      }
    }
  }
}
</script>

<style scoped>
.itemWrapper {
  height: 40px;
  width: 100%;
  padding: 8px 5px;
  box-sizing: border-box;
  margin: 8px 0;
  background: #fdcb6e;
  overflow: hidden;

  border-radius: 5px;

  transition: all .1s;

  user-select: none;

}

.itemWrapper:hover {
  background: #d6ab5c;
}

.itemWrapper:hover button {
  display: inline-block;
}

.itemWrapper > li, label {
  display: inline-block;
  height: 100%;
  width: 100%;
}

.itemWrapper > li > label {
  display: inline-block;
  width: 80%;
  height: 100%;
}

.itemWrapper > li > label > input {
  vertical-align: middle;
}

.itemWrapper button {
  line-height: 1;
  font-size: 13px;
  float: right;
  height: 25px;
  display: none;
}
</style>