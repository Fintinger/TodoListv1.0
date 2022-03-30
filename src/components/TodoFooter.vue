<template>
  <div class="todoFooter" v-show="total">
    <label for="">
<!--      <input type="checkbox" :checked="isAll"  @change="handleCheckAll">-->
      <input type="checkbox" v-model="isAll">
      <span>已完成 <span>{{ completedNum }}</span> / 全部 <span>{{ total }}</span></span>
    </label>
    <button class="btn_danger" @click="handleDelAll">清除已完成任务</button>
  </div>
</template>

<script>
export default {
  name: "TodoFooter",
  props: ["todos"],
  computed: {
    completedNum() {
      return this.todos.filter(el => el.completed === true).length
      // return this.todos.reduce((i, el) => i + (el.completed ? 1 : 0),0)
    },
    total() {
      return this.todos.length
    },
    isAll:{
      get(){
        return this.completedNum === this.total && this.total > 0
      },
      set(value){
        // this.checkAll(value)
        this.$emit("checkAll",value)
      }
    }
  },
  methods: {
/*    handleCheckAll(e) {
      this.checkAll(e.target.check)
    },*/
    handleDelAll() {
      if (confirm("是否删除所有已完成项？"))
        // this.DelAll()
        this.$emit("DelAll")
    }
  }
}
</script>

<style scoped>
.todoFooter {
  margin: 5px 0;
  height: 30px;
  line-height: 30px;
}

.todoFooter > label {
  display: inline-block;
  width: 200px;
  height: 100%;
}

.todoFooter > label > input {
  vertical-align: middle;
}

.todoFooter > label > span > span {
  color: #e01;
  font-weight: 700;
  font-size: 15px;
}

.todoFooter > button {
  float: right;
}
</style>