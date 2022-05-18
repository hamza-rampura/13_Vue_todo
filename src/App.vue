<template>
  <div id="app">
      <HeaderMain />
      <AddToDo v-on:add-todo = "addTodo"/>
      <TodosBase v-bind:todos="todos" v-on:del-todo="deleteTodo" v-on:change-status="changeStatus" />
  </div>
</template>

<script>

import TodosBase from "./components/TodosBase.vue";
import HeaderMain from "./components/layout/HeaderMain.vue";
import AddToDo from "./components/AddToDo.vue";

export default {
  name: 'App',
  components: {
      TodosBase,
      HeaderMain,
      AddToDo
  },
  data() {
      return {
          todos: [
              {
                  id: 1,
                  title: "Hamza",
                  completed: false
              },
              {
                  id: 2,
                  title: "Hamza2",
                  completed: false
              },
              {
                  id: 3,
                  title: "Hamza3",
                  completed: false
              }
          ],
          test: "Hamza"
      }
  },
  methods: {
        deleteTodo(id) {
            this.todos = this.todos.filter((todo)=>{
                return todo.id !== id;
            })
        },
        changeStatus(id) {
            for(let i = 0; i<=this.todos.length; i++) {
                if(this.todos[i].id === id) {
                  this.todos[i].completed = !this.todos[i].completed;
                  return;
                }
            }
        },
        addTodo(newTodo) {
            this.todos = [...this.todos, newTodo]
            console.log(this.todos)
        }
  }
}
</script>

<style>
* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }
  .btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }
  .btn:hover {
    background: #666;
  }
</style>
