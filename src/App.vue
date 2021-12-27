<template>
  <div class="todo-container">
    <div class="todo-wrap">
      <Header @getToDo="getToDo"/>
      <List :todos="todos" :getIsChecked="getIsChecked" :deleteItem="deleteItem"/>
      <Footer :todos="todos" :deleteFinish="deleteFinish" :handleIsAllCheck="handleIsAllCheck"/>
    </div>
  </div>
</template>

<script>
import Header from "@/components/Header.vue"
import List from "@/components/List.vue"
import Footer from "@/components/Footer.vue"
export default {
  data(){
    return {
    //   todos:[
    //     {
    //       id:1,
    //       content:'预习vue',
    //       isDone:true
    //     },
    //     {
    //       id:2,
    //       content:'学习vue',
    //       isDone:false
    //     },
    //     {
    //       id:3,
    //       content:'复习vue',
    //       isDone:false
    //     }
    //   ]
    todos:JSON.parse(localStorage.getItem('TODOS')) || []
    }
  },
  components:{
    Header,
    List,
    Footer
  },
  methods:{
    // 获取任务数据
    getToDo(data){
      this.todos.unshift(data);
    },
    // 获取checkbox的value，根据当前的index来更改数据
    getIsChecked(isChecked,index){
      this.todos[index].isDone = isChecked; 
    },
    // 删除要删除的数据
    deleteItem(index){
      this.todos.splice(index,1);
    },
    // 删除所有已经完成的
    deleteFinish(){
      this.todos = this.todos.filter(v => v.isDone !== true);
    },
    // 处理是否AllCheck
    handleIsAllCheck(checked){
      this.todos = this.todos.map(v => {
        v.isDone = checked
        return v
        });
    },
  },
  watch:{
    todos:{
      deep:true,
      handler(newVal){
        // 当todos数据发生改变的时候，就将变化后的数据存储带哦localStorage当中
        // localStorage是前端本地存储的方案，是一个小型的数据库，存储到localStorage当中的东西都会自动住哪胡为字符串
        // local有四个API
        localStorage.setItem('TODOS',JSON.stringify(newVal));
      }
    }
  }
}
</script>

<style>
  /*base*/
body {
  background: #fff;
}

.btn {
  display: inline-block;
  padding: 4px 12px;
  margin-bottom: 0;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
}

.btn-danger {
  color: #fff;
  background-color: #da4f49;
  border: 1px solid #bd362f;
}

.btn-danger:hover {
  color: #fff;
  background-color: #bd362f;
}

.btn:focus {
  outline: none;
}
/*app*/
.todo-container {
  width: 600px;
  margin: 0 auto;
}
.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
</style>