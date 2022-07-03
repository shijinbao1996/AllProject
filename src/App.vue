<template>
  <div class="todoapp">
     <TodoHeader @add='addFn'></TodoHeader>
     <!-- @setchecked="setcheckedFn" -->
     <TodoMain :list='showlist' @del='delFn'></TodoMain>
     <TodoFooter :count='count' @filterdata='filterdataFn' @clear='clearFn'></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoMain from './components/TodoMain.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  components:{
    TodoHeader,
    TodoMain,
    TodoFooter
  },
  data(){
    return{
      list: JSON.parse(localStorage.getItem("list"))||[],
      getSel:'all'
    }
  },
  methods:{
    addFn(val){
      let id = this.list[0]? this.list[this.list.length-1].id+1:100
      this.list.push({
        id,
        name:val,
        isDone:false
      })
    },
    delFn(id){
     const index = this.list.findIndex((ele) => ele.id=id)
     this.list.splice(index,1)
    },
    filterdataFn(val){
      // 根据 val list
      console.log(val);
      this.getSel = val ;
      // list 是不是根据 val不同值 显示不同的list
    },
    clearFn(){
      this.list.forEach((ele) => (ele.isDone=false))
    },
    // setcheckedFn(val) {
    //   this.list.forEach((ele) => (ele.isDone = val))
    // }
  },
  computed:{
    count(){
      return this.list.filter((ele) => !ele.isDone).length
    },
    showlist(){
      if(this.getSel == 'no') {
        return this.list.filter((ele)=> !ele.isDone);
      } else if (this.getSel == 'yes') {
        return this.list.filter((ele)=> ele.isDone);
      } else {
        return this.list
      }
    }
  },
  watch:{
    list:{
      deep:true,
      handler(val){
        localStorage.setItem("list",JSON.stringify(val || []))
      }
    }
  }
}
</script>

<style>

</style>
