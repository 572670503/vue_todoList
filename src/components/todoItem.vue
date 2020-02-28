<template>
          <li :class={light:light} @mouseenter="light=true"
                                 @mouseleave="light=false"
          >
            <label>
              <input type="checkbox" v-model="checked"/>
              <span>{{item.content}}</span>
            </label>
            <button class="btn btn-danger" v-show="light"
            @click="delTodo">删除</button>
            
          </li>
</template>

<script>
export default {   
  name: 'todoItem',
  props:{
    item:Object
  },
  data(){
    return {
         light:false
    }
  },
  computed:{
    checked:{
      get(){
        return this.item.checked
      },
      set(val){
        this.bus.$emit("change",this.item.id,val)
      }
    }
  },
  methods:{
    delTodo(){
      //把id传给app，进行删除
      this.bus.$emit("delTodo",this.item.id)
    }
  }
}
</script>

<style scoped>
.light{
  background-color: pink;
}
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}

li label {
  float: left;
  cursor: pointer;
}

li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}

li button {
  float: right;
  /* display: none; */
  margin-top: 3px;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}

</style>
