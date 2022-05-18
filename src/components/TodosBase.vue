<template>
    <div>
        <div v-bind:key="todo.id" v-for="todo in todos">
            <TodosItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo.id)" v-on:change-status="$emit('change-status', todo.id)"/> <!--  todo_prop.sync="todo" -->
        </div>


    </div>
</template>

<script>
import TodosItem from "./TodosItem.vue"
export default {
    name: "TodosBase",
    components: {
        TodosItem
    },
    props: ["todos"]
}
</script>

<style scoped>

</style>