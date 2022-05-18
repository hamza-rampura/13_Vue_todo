<template>
    <div class="todo-item" v-bind:class="{'is-complete':todo.completed}">
        <input type="checkbox" @click="$emit('change-status', todo.id)">
        <p>{{todo.title}}</p>
        <button @click="$emit('del-todo', todo.id)" class="del">x</button>
    </div>
</template>

<script>
export default {
    name: "TodosItem",
    props: ["todo"],
    methods: {
        markComplete() { 
            console.log("Complete/Incomplete " + this.todo.id);
            /* this.todo.complete = !this.todo.complete; */
            /* This gives us an error as Unexpected mutation of "todo" prop */
        }
    }
}
</script>

<style scoped>
.todo-item {
    background: #f4f4f4;
    padding: 10px;
    border-bottom: 1px #ccc dotted;
    display: flex;
    width: 100%;
    align-items: center;
    justify-content: space-between;
  }
  .is-complete {
    text-decoration: line-through;
  }
  .del {
    background: #ff0000;
    color: #fff;
    border: none;
    padding: 5px 9px;
    border-radius: 50%;
    cursor: pointer;
    float: right;
  }

</style>

