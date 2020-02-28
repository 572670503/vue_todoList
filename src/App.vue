<template>
   <div id="app">
      <div class="todo-container">
         <div class="todo-wrap">
              <todo-header @addTodo="addTodo"></todo-header>
              <todo-list :listArr="listArr"></todo-list>
              <todo-footer></todo-footer>
      </div>
    </div>
  </div>
</template>

<script>
import todoHeader from "./components/todoHeader"
import todoList from "./components/todoList"
import todoFooter from "./components/todoFooter"
export default {
  name: 'App',
  data(){
      return{
        listArr:[
          {id:0,content:"新恒结衣",checked:false},
          {id:1,content:"黑坂优香子",checked:false},
          {id:2,content:"花泽香菜",checked:false}
        ]
      }
    },
  components:{
     "todo-header":todoHeader,
     "todo-list":todoList,
     "todo-footer":todoFooter
  }, 
  methods:{
    addTodo(item){
      this.listArr.unshift(item)
    }
  },
  mounted(){
     this.bus.$on("delTodo",(id)=>{
          this.listArr = this.listArr.filter((item)=>{
              return  item.id!== id
          })
     })
     this.bus.$on("change",(id,checked)=>{
        this.listArr.forEach((item)=>{
            if(item.id===id){
              item.checked = checked
            }
         })
     })
}
}

</script>

<style>
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
