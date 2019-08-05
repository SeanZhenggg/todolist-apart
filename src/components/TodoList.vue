<template>
  <div id="list">
    <ul>
      <li v-for="todo in todos" :key="todo.id" v-bind:class="{'Completed' : todo.completed}">
        <div v-if="cachedTodo.id != todo.id">
          <input type="checkbox" v-model="todo.completed" />
          {{todo.title}}
        </div>
        <div v-else id="input">
          <input type="text" v-model="todo.title" />
        </div>
        <div>
          <div v-if="cachedTodo.id != todo.id">
            <button v-on:click="editTodo(todo)">edit</button>
            <button v-on:click="$emit('delete:todo',todo.id)">delete</button>
          </div>
          <div v-else>
            <button v-on:click="saveTodo">Save</button>
            <button v-on:click="cancelTodo(todo)">Cancel</button>
          </div>
        </div>
      </li>
    </ul>
    <div id="bottom">
      <span>還有 {{todos.length}} 項任務未完成</span>
      <a href="#" @click.prevent="$emit('delete:all')">清除所有任務</a>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoList",
  props: {
    todos: Array
  },
  data: function() {
    return {
      cachedTodo: {},
      cachedTitle: ""
    };
  },
  methods: {
    editTodo(todo) {
      this.cachedTodo = todo;
      this.cachedTitle = todo.title;
    },
    saveTodo() {
      this.cachedTodo = {};
    },
    cancelTodo(todo) {
      todo.title = this.cachedTitle;
      this.cachedTodo = {};
    }
  }
};
</script>

<style scoped>
#list{
    width: 500px;
}
li {
  display: flex;
  flex-flow: row;
  justify-content: space-between;
  align-items: center;
}
.Completed {
  text-decoration: line-through;
}
ul {
  list-style-type: none;
  padding: 0;
}
#input {
  width: 70%;
}
#input input {
  width: 100%;
}
#bottom{
  display: flex;
  flex-flow: row;
  justify-content: space-between;
  align-items: center;
}
a{
  text-decoration: none;
}
</style>


