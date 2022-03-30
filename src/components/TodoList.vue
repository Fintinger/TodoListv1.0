<template>
 <div class="listContainer">
   <ul>
     <TodoItem
         v-for="todo in todos"
         :key="todo.id"
         :todo="todo"
     />
   </ul>
 </div>
</template>

<script>
import TodoItem from "@/components/TodoItem";

export default {
  name: "TodoList",
  components:{TodoItem},
  props:["todos"]
}
</script>

<style scoped>

</style>