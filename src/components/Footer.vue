<template>
  <div class="todo-footer">
    <label>
      <input type="checkbox" :checked="isChecked" @change="handleIsAllFinished"/>
    </label>
    <span>
      <span>{{finish}}</span> / {{total}}
    </span>
    <button class="btn btn-danger" @click="handleDelete">删除已完成</button>
  </div>
</template>

<script>
export default {
  props:["todos","deleteFinish","handleIsAllCheck"],
  methods:{
    // 点击按钮全部完成或者全部不完成
    handleIsAllFinished(event){
      const {checked} = event.target;
      this.handleIsAllCheck(checked);
    },
    // 删除所有已经完成的
    handleDelete(){
      this.deleteFinish();
    },
  },
  computed:{
    total(){
      return this.todos.length;
    },
    finish(){
      return this.todos.filter(v => v.isDone === true).length;
    },
    isChecked(){
      if(this.finish === this.total && this.total !== 0){
        return true
      }else{
        return false
      }
    }
  }
}
</script>

<style>
  /*footer*/
  .todo-footer {
    height: 40px;
    line-height: 40px;
    padding-left: 6px;
    margin-top: 5px;
  }

  .todo-footer label {
    display: inline-block;
    margin-right: 20px;
    cursor: pointer;
  }

  .todo-footer label input {
    position: relative;
    top: -1px;
    vertical-align: middle;
    margin-right: 5px;
  }

  .todo-footer button {
    float: right;
    margin-top: 5px;
  }
</style>