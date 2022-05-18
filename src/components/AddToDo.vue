<template>
    <div>
        <form @submit="addToDo">
            <input type="text" name="title" v-model="title" placeholder="Add to Do">
            <input type="submit" value="Submit" class="btn">
        </form>
    </div>
</template>

<script>
// import uuid from "uuid"
export default {
    name: "AddToDo",
    data() {
      return {
          title: ""
      }  
    },
    methods: {
        addToDo(e) {
            e.preventDefault();
            const newToDo = {
                id: 123,
                title: this.title,
                completed: false
            }
            // Send to parent
            this.$emit("add-todo", newToDo)
        }
    }
}
</script>

<style scoped>
  form {
    display: flex;
  }
  input[type="text"] {
    flex: 10;
    padding: 5px;
  }
  input[type="submit"] {
    flex: 2;
  }
</style>