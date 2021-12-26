<template>
   <ul class="todo-main">
     <Item v-for="(todoItem,index) in todos" :key="todoItem.id" :index="index" :todoItem="todoItem" :getIsChecked="getIsChecked" :deleteItem="deleteItem"/>
  </ul>
</template>

<script>
import Item from "./Item.vue"
export default {
  props:["todos","getIsChecked","deleteItem"],
  components:{
    Item,
  }
}
</script>

<style>

</style>