<template>
 <div>
  <form @submit.prevent>
 <input v-bind:value="text"
 
 @input="text=$event.target.value"
 />
  <button @click="createTodo">Добавить задачу</button>
  </form>
 
<div v-for="todo in todos" :key="todo.id">

<input type="checkbox" id="checkbox" v-model="checked" onchange="toggleTodo" />
<label for="checkbox">{{ checked }}</label>
<span>{{todo.text}}</span>
<button @click="removeTodo">Delete</button>
</div> 
<button @click="isActive">Активные</button>    
<button @click="all">Все</button>
<button @click="isCompleted">Завершенные</button>
 </div>
</template>
<script>
import axios from 'axios'
export default{
  data(){
    return {
      todos:[],
    
    }
  },
  methods:{
createTodo(){
const newTodo={
  id:Date.now(),
  text:this.text,
  active:false
}
this.todos.push(newTodo)
this.text=""
},
removeTodo(id){
this.todos.splice(id, 1)
console.log(id)
},
toggleTodo(){
this.active=!this.active
},
all(){

},
isActive(){

},
isCompleted(){

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
    }
}
</script>
<style>

</style>
