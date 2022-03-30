<template>
  <div class="itemWrapper ">
    <li>
      <label>
        <input :checked="todo.completed" type="checkbox" @change="handleCheck(todo.id)">
        <span v-show="!todo.isEdit" :class="{textLineThrough: todo.completed}" :title="todo.name">{{ todo.name }}</span>
        <input
            class="editBox"
            type="text"
            v-show="todo.isEdit"
            ref="inputTitle"
            :value=todo.name
            @blur="handleBlur(todo)"
            @keyup.enter="handleBlur(todo)"
        >
      </label>
      <button class="btn_danger" @click="handleDelete(todo.id)">删除</button>
      <button v-show="!todo.isEdit" class="btn_edit" @click="handleEdit(todo)">编辑</button>
    </li>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    handleCheck(id) {
      //通知App组件改变对应todo的completed值
      // this.checkTodo(id);
      this.$bus.$emit('checkTodo', id)
    },
    handleDelete(id) {
      //通知App组件删除对应todo项
      if (confirm("是否删除该项？")) {
        this.$bus.$emit('delTodo', id)
      }
    },
    handleEdit(todo) {
      //使用内置方法修改，以免破坏数据监听
      // eslint-disable-next-line no-prototype-builtins
      if (!todo.hasOwnProperty('isEdit')) {
        this.$set(todo, 'isEdit', true)
      }
      todo.isEdit = true;

      //让输入框聚焦
      this.$nextTick(() => this.$refs.inputTitle.focus())
    },
    handleBlur(todo) {
      //修改编辑状态
      todo.isEdit = false;
      //更改内容
      if (!this.$refs.inputTitle.value.trim()) alert('输入内容不能为空!')
      this.$bus.$emit('updateTodo', todo.id, this.$refs.inputTitle.value)
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
  width: 70%;
  height: 100%;
  overflow: hidden;
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

.itemWrapper .editBox {
  height: 100%;
  width: 70%;
  padding-left: 5px;
  box-sizing: border-box;
}

.textLineThrough {
  text-decoration: line-through;
}
</style>