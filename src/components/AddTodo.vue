<template>
  <div>
      <form @submit="addTodo">
          <input type="text" v-model="title" name="title" placeholder="Add Todo...">
          <input type="submit" value="Submit" class="btn">
      </form>
  </div>
</template>

<script>
// https://www.npmjs.com/package/uuid
// Jsonplaceholder provides unique id. So we are not using it now
// import { v4 as uuidv4 } from 'uuid';

export default {
    name: "AddTodo",
    data() {
        return {
            title: ''
        }
    },
    methods: {
        addTodo: function(e){
            // Stoping default behavior
            e.preventDefault();
            const newTodo = {
                // id: uuidv4(),
                title: this.title,
                completed: false
            }
            // send up to parent
            this.$emit('add-todo', newTodo);
            this.title = '';
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