<template>
   <div class="todo-header">
      <input type="text" placeholder="请输入你的任务名称，按回车键确认" v-model="content" @keyup.enter="handleToDo"/>
    </div>
</template>

<script>
export default {
  data(){
    return {
      content:'',
    }
  },
  methods:{
    handleToDo(){
      const {content} = this;
      if(content.trim()){
        // 将数据传递给父组件
        const data = {
          id:Date.now(),
          content:content.trim(),
          isDone:false
        }
        this.$emit("getToDo",data);
        this.content = '';
      }else{
        alert("请检查输入")
      }
    },
  }
}
</script>

<style>
  /*header*/
  .todo-header input {
    width: 560px;
    height: 28px;
    font-size: 14px;
    border: 1px solid #ccc;
    border-radius: 4px;
    padding: 4px 7px;
  }

  .todo-header input:focus {
    outline: none;
    border-color: rgba(82, 168, 236, 0.8);
    box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 8px rgba(82, 168, 236, 0.6);
  }
</style>