<template>
          <li>
            <label>
              <input type="checkbox" v-model="checked" @change="change(item.id)"/>
              <span>{{item.content}}</span>
            </label>
            <button class="btn btn-danger" style="display:none">删除</button>
          </li>
</template>

<script>
export default {   
  name: 'todoItem',
  props:{
    item:Object
  },
  data(){
    return{
      checked:this.item.checked
    }
  },
  methods:{
    //当前这个函数被调用时，我们要去修改app中的checked数据
    change(id){
      this.bus.$emit("change",id,this.checked)
    }
  }
}
</script>

<style scoped>
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
  display: none;
  margin-top: 3px;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}

</style>
