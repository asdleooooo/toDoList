<template>
  <li @mouseenter="handleMouse('enter')" @mouseleave="handleMouse('leave')">
      <label>
        <input type="checkbox" :checked="todoItem.isDone" @change="handleChange"/>
        <span>{{todoItem.content}}</span>
      </label>
      <button class="btn btn-danger" v-show="isEnter" @click="handleDelete">删除</button>
    </li>
</template>

<script>
export default {
  data(){
    return {
      isEnter:false,
    }
  },
  props:{
    index:Number,
    todoItem:Object,
    getIsChecked:Function,
    deleteItem:Function,
  },
  methods:{
    handleMouse(type){
      if(type === 'enter'){
        this.isEnter = true;
      }else if(type === 'leave'){
        this.isEnter = false;
      }
    },
    handleChange(event){
      const {checked} = event.target;
      this.getIsChecked(checked,this.index);
    },
    handleDelete(){
      this.deleteItem(this.index);
    },
  }
}
</script>

<style>

</style>