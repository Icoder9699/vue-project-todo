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
    <todo-add
      @addTodo="addTodoHandler"
    />
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

  export default{
    data(){
      return {
        todos: [
          {id: 1, title: 'Hello', completed: true},
          {id: 2, title: 'Vue', completed: false},
          {id: 3, title: 'Easy-vue', completed: false}
        ],
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
    },
    methods: {
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
    created(){
      // fetch('https://jsonplaceholder.typicode.com/todos/')
      //   .then(response => response.json())
      //   .then(json => console.log(json))
        
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
#app{
  width: 500px;
  margin: 100px auto;
}

</style>
