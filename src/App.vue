<template>
  <div id="app">
    <div id="top">
      <h1>TodoList</h1>
      <input-todo v-on:add:newtodo='addNewTodo'></input-todo>
    </div>
    <todo-nav v-on:show:view="showView"></todo-nav>
    <todo-list :todos="filterTodos" v-on:delete:todo="deleteTodo" v-on:delete:all="deleteAll"></todo-list>
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue'
import InputTodo from './components/InputTodo.vue'
import TodoNav from './components/TodoNav.vue'

export default {
  name: 'app',
  components: {
    TodoNav,
    InputTodo,
    TodoList,
  },
  data:function(){
    return{
      Todos : [
        {
          id:345,
          title:'The First Thing To Do Today',
          completed:false,
        },
        {
          id:678,
          title:'The Second Thing To Do Today',
          completed:false,
        },
        {
          id:912,
          title:'The Third Thing To Do Today',
          completed:false,
        },
      ],
      visibility : 'all',
    }
  },
  methods:{
    deleteAll(){
      this.Todos = [];
    },
    addNewTodo(value){
      let newId = Math.floor(Date.now());
      this.Todos.push({
        id:newId,
        title:value,
        completed:false,
      });
    },
    showView(value){
      this.visibility = value;
    },
    deleteTodo(todoId){
      let chooseDeleted = '';
      this.Todos.forEach(function(item,key){
      if(item.id === todoId){
          chooseDeleted = key;
        }});
        // console.log(chooseDeleted);
      this.Todos.splice(chooseDeleted,1);
    }
  },
  computed:{
    filterTodos(){
       if(this.visibility == 'ing'){
        let NewfilterTodo = [];
        this.Todos.forEach(function(item){
          if(item.completed == false){
            NewfilterTodo.push(item);
          }
        });
        return NewfilterTodo;
      }
      else if(this.visibility == 'done'){
        let NewfilterTodo = [];
        this.Todos.forEach(function(item){
          if(item.completed == true){
            NewfilterTodo.push(item);
          }
        });
        return NewfilterTodo;
      }
      return this.Todos;
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  height:500px;
  display:flex;
  flex-flow: column;
  justify-content: space-around;
  align-items: center;
}
#top{
  display:flex;
  width:300px;
  height:100px;
  flex-flow: column;
  justify-content: space-evenly;
  align-items: center;
  padding:30px;
  border:1px solid #444444;
}
</style>
