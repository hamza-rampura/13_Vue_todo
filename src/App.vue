<template>
	<div id="app">
		<HeaderMain />
		<AddToDo v-on:add-todo="addTodo" />
		<TodosBase
			v-bind:todos="todos"
			v-on:del-todo="deleteTodo"
			v-on:change-status="changeStatus"
		/>
	</div>
</template>

<script>
	import TodosBase from "./components/TodosBase.vue";
	import HeaderMain from "./components/layout/HeaderMain.vue";
	import AddToDo from "./components/AddToDo.vue";
	import axios from "axios";

	export default {
		name: "App",
		components: {
			TodosBase,
			HeaderMain,
			AddToDo,
		},
		data() {
			return {
				todos: [],
				test: "Hamza",
			};
		},
		methods: {
			deleteTodo(id) {
				axios
					.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
					.then(() => {
						this.todos = this.todos.filter((todo) => {
							return todo.id !== id;
						});
					})
					.catch((err) => console.log(err));
			},
			changeStatus(id) {
				for (let i = 0; i <= this.todos.length; i++) {
					if (this.todos[i].id === id) {
						this.todos[i].completed = !this.todos[i].completed;
						return;
					}
				}
			},
			addTodo(newTodo) {
				const { title, completed } = newTodo;
				axios
					.post("https://jsonplaceholder.typicode.com/todos", {
						title,
						completed,
					})
					.then((res) => (this.todos = [...this.todos, res.data]))
					.catch((err) => console.log(err));
			},
		},
		created() {
			axios
				.get("https://jsonplaceholder.typicode.com/todos?_limit=5")
				.then((res) => {
          this.todos = res.data;
				})
				.catch((err) => console.log(err));
		},
	};
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
