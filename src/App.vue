<template>
 <div>
  <form @submit.prevent>
 <input v-bind:value="text"
 
 @input="text=$event.target.value"
 />
  <button @click="createTodo">Добавить задачу</button>
  </form>
 
<div v-for="todo in todosFiltered" :key="todo.id">

<input type="checkbox" v-model="todo.active" />
<span>{{todo.text}}</span>
<button @click="removeTodo">Delete</button>
</div> 
<button  @click="filterBy='active'">Активные</button>    
<button @click="filterBy='all'">Все</button>
<button @click="filterBy='completed'">Завершенные</button>
 </div>
</template>
<script>
import axios from 'axios'
export default{
  data(){
    return {
      todos:[],
      filterBy:"all"
    
    }
  },
  methods:{
    // create new Todo//
createTodo(){
const newTodo={
  id:Date.now(),
  text:this.text,
  active:false
}

this.todos.push(newTodo)
this.text=""
},

// delete Todo  //
removeTodo(id){
this.todos.splice(id, 1)
console.log(id)
},


async fetchTodos(){
      try{
const response = await axios.get('https://my-json-server.typicode.com/falk20/demo/todos')
this.todos=response.data
console.log(response)
      }catch(e){
        alert('Error')
      }
    }
    
  },
  mounted(){
      this.fetchTodos()
    },
    computed:{
todosFiltered(){
  if(this.filterBy =="all"){
    return this.todos
  }else if(this.filterBy=="active"){
return this.todos.filter(todo=>!todo.active)
  }else if(this.filterBy=="completed"){
    return this.todos.filter(todo=>todo.active)
  }
  return this.todos
}
}
}
</script>
<style>

</style>
