<template>
  <header class="header">
    <h1>todos</h1>
    <input id="toggle-all" class="toggle-all" type="checkbox" v-model="isAll">
    <label for="toggle-all"></label> 
    <!-- label 可以关联一个表单标签 -->
    <input
      class="new-todo"
      placeholder="输入任务名称-回车确认"
      autofocus
      v-model.trim="task"
      @keyup.enter='enter'
    />
  </header>
</template>

<script>
export default {
  data(){
    return{
      task:''
    }
  },
 methods:{
  enter(){
    if(this.task.length == 0) {
      return alert ('请输入')
    }
    this.$emit('add',this.task)
    this.task = ''
  }
 },
 computed:{
  isAll:{
     get(){
      //取值 list里边值
      // this.$parent 父组件 every 找错 一个错全错 全对才对
      return this.$parent.list.every((ele) => ele.isDone)
     },
     set(checked) {
      // 子到父
      // this.$emit("setchecked",checked);

      // 在子组件 直接改父组件里边值
      this.$parent.list.forEach((ele) => (ele.isDone = checked))
     }
 }
 }
}
</script>