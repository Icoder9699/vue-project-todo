<template>
  <div id="app">
    <h1>Todo-application</h1>
    <span style="margin: 0 10px 0 0">
      <strong>Todos:</strong>
      {{todos.length}}
    </span>
    <span style="color: red">
      <strong>Completed</strong> : {{ completedTodos }}
    </span>
    <my-modal 
      v-if="show"
      @addTodo="addTodoHandler"
      @showModal="showModal" 
    />
    <button 
      class="btn btn-create"  
      @click="showModal" 
      v-else
    >
      Create Todo
    </button>

    <h3 v-if="isLoading">Loading...</h3>
    <todo-list 
      v-if="todos.length > 0"
      :todos="todos"
      @removeTodo="removeTodoHandler"
      @completeTodo="completeTodoHandler"
    />
    <h2 v-else style="text-align: center">Todos for today 0</h2>
  </div>
</template>
  
<script>
import TodoAdd from './components/TodoAdd.vue'
import TodoList from './components/TodoList.vue'
import MyModal from './components/UI/MyModal.vue'
import axios from 'axios'
  export default{
    data(){
      return {
        todos: [],
        show: false,
        isLoading: true
      }
    },
    computed: {
      completedTodos() {
        const completed = this.todos.filter(({ completed }) => completed === true);
        
        return completed.length;
      }
    },
    components: {
      TodoList,
      TodoAdd,
        MyModal,
    },
    methods: {
      showModal(){
        this.show = !this.show
      },
      removeTodoHandler(id){
        this.todos = this.todos.filter(todo => todo.id !== id)
      },
      completeTodoHandler(id){
        this.todos = this.todos.map(todo => {
          if(todo.id === id){
             todo.completed = !todo.completed
          }
          return todo
        })
      },
      addTodoHandler(todo){
        this.todos.push(todo)
      }
    },
    async created(){
      setTimeout(async () => {
        const todos = await axios('https://jsonplaceholder.typicode.com/todos?&_limit=10')
        this.todos = todos.data
        this.isLoading = false
      }, 3000)
    }
  }
</script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;500;700&display=swap');

*{
  margin: 0;
  box-sizing: border-box;
}
body{
  margin: 0;
  padding: 0;
  font-family: 'Poppins';
}
h1{
  margin: 10px 0;
  text-align: center;
}
.btn {
  width: 100%;
  height: 40px;
  background: transparent;
  transition: all 300ms linear;
  border: 1px solid rgb(108, 91, 199);
  color: rgb(108, 91, 199);
  cursor: pointer;
}
.btn:hover{
  background-color: rgb(108, 91, 199);
  color: #fff;
}
#app{
  width: 500px;
  margin: 100px auto;
}

</style>
