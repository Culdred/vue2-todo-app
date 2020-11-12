<template>
  <div id="app">
    
    <div class="container">

      <div class="header">
        <img alt="Vue logo" src="./assets/logo.png">
        <div class="">{{ title }}</div>
      </div>

      <div class="break-row"></div>

      <div class="features">
        <form @submit.prevent="addTodo">
          <label for="newTodo">New Todo</label>
          
          <div class="break-row"></div>
          
          <input v-model="newTodo" type="text" name="newTodo" id="newTodo" placeholder="Add something...">
          <button type="submit" name="button">Add</button>
        </form>
        
        <div class="break"></div>
        
        <button @click="allDone" type="button" class="">All done!</button>
        <button @click="allUndone" type="button" class="">All undone!</button>
      </div>

      <div class="break-row"></div>
      
      <ul class="">
        <li v-for="(todo, idx) in todos" :key="idx" class="main">

          <input v-model="todo.done" type="checkbox" name="" id="">
          <span :class="{ done: todo.done }">{{ todo.title }}</span>

          <button @click="moveTodo(todo, 'up')" type="button">↑</button>
          <button @click="moveTodo(todo, 'down')" type="button">↓</button>
          <button @click="removeTodo(todo)" type="button">Del</button>

        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data: function() {
    return {
      title: "Todo App",
      newTodo: "",
      todos: []
    }
  },
  methods: {
    addTodo() {
      if(this.newTodo !== "") {
        this.todos.push({
          title: this.newTodo,
          done: false
        });
        this.newTodo = "";
      }
    },
    allDone() {
      this.todos.forEach(function(todo) {
        todo.done = true;
      })
    },
    allUndone() {
      this.todos.forEach(function(todo) {
        todo.done = false;
      })
    },
    removeTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos.splice(todoIndex, 1);
    },
    moveTodo(todo, direction) {
      let currIdx = this.todos.indexOf(todo);
      let prevIdx = currIdx - 1;
      let nextIdx = currIdx + 1;
      let currElement = this.todos[currIdx];
      let prevElement = this.todos[prevIdx];
      let nextElement = this.todos[nextIdx];
      if(prevIdx > -1 && direction === "up") {
          this.todos.splice(prevIdx, 1, currElement);
          this.todos.splice(currIdx, 1, prevElement);
      } else if (nextIdx < this.todos.length && direction === "down") {
          this.todos.splice(nextIdx, 1, currElement);
          this.todos.splice(currIdx, 1, nextElement);
      }
    },
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  /* color: #2c3e50; */
  color: white;
  margin-top: 60px;
}
#newTodo {
  margin: 5px;
  padding: 8px;
}
.container {
  display: flex; /* or inline-flex */
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  /* border: 1px solid purple; */
}
.header {
  /* border: 1px solid purple; */
}
.features {
  /* border: 1px solid purple; */
}
.main {
  /* border: 1px solid purple; */
}
.left-group {
  /* border: 1px solid purple; */
}
.right-group {
  /* border: 1px solid purple; */
}
.break-row {
  flex-basis: 100%;
  height: 0;
  /* border: 1px solid purple; */
}
.done {
  text-decoration: line-through;
}
body {
  background-color: teal;
}
span {
  margin: 10px;
}
ul {
  list-style: none;
}
input {
  border: 1px solid rgb(10, 75, 75);
  border-radius: 2px;
}
button {
  background-color: rgb(10, 75, 75);
  border: 1px solid rgb(10, 75, 75);
  color: white;
  text-align: center;
  transition-duration: 0.4s;
  margin: 2px;
  padding: 8px;
  border-radius: 2px;
  outline: none;
}
button:hover {
  background-color: white;
  color: rgb(10, 75, 75);
}
</style>