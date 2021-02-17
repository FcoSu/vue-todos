<template>
  <div class="grid-container">
    <div id="header" class="header">

    <Search v-on:query-change="querySearch"/>
    </div>
    <div id="main-container" class="body">
      <h2>Todos</h2>
      <TodoAdd v-on:add-todo="addTodo"/>
      <Todos v-bind:todosList="copyTodos" v-on:delete-todo="deleteTodo"/>
    </div>
  </div>
</template>

<script>
import Search from "./components/Search";
import Todos from "./components/Todos";
import TodoAdd from "./components/TodoAdd";

export default {
  name: 'App',
  components: {
    Todos,
    TodoAdd,
    Search
  },
  methods: {
    deleteTodo(id){
      this.todos = this.todos.filter(todo => todo.id != id);
      this.copyTodos = [ ... this.todos]
    },
    addTodo(todo){
      this.todos.push(todo);
      this.copyTodos = [ ... this.todos];
    },
    querySearch(query){
      if(query.trim()===''){
        this.copyTodos = [ ... this.todos];
      }else{
        const temp = this.todos.filter(todo => {
          return todo.title.includes(query)
        });

        this.copyTodos = [ ... temp]
      }
    }
  },
  data(){
    return {
      todos:[
        {
          id: 0,
          title: 'comprar la cena',
          completed: false
        },
        {
          id: 1,
          title: 'Alimentar al perro',
          completed: true
        },
        {
          id: 2,
          title: 'Jugar LOL',
          completed: false
        },
        {
          id: 3,
          title: 'Terminar tutorial',
          completed: true
        }
      ],
      copyTodos:[]
    }
  },
  created(){
    this.copyTodos = [...this.todos];
  }
}
</script>

<style>
.grid-container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-template-rows: 0.6fr 1.7fr 0.7fr;
  gap: 0px 0px;
  grid-template-areas:
    ". header header ."
    ". body body ."
    ". . . .";
}
.header { grid-area: header; }
.body { grid-area: body; }




*{
  box-sizing: border-box;
}


body{
  font-family: 'Courier New', Courier, monospace;
  font-size: 1.5em;
  padding:0;
  margin: 0;
}


#main-container{
  border: solid 1px #ccc;
  width: 600px;
  margin: 100px auto;
}

#header{
  background: black;
  padding:  10px;
}

h2{
  padding: 0 10px;
}
</style>
