<template>
  <div class="container">
    <div class="add-todo">
      <span>Add new Item</span>
      <input type="text" v-model="todoText" />
      <button @click="submitToDo">Submit</button>
    </div>

    <div class="todo-list">
      <ToDoListItem v-for="todo in todos" :item="todo" :key="todo.id" />
    </div>
  </div>
</template>

<script>
import axios from 'axios';

import ToDoListItem from './ToDoListItem.vue';

export default {
  components: {
    ToDoListItem,
  },
  data() {
    return {
      todoText: '',
      todos: [],
    };
  },
  methods: {
    submitToDo() {
      const item = { isOpen: true, text: this.todoText };
      (async () => {
        await axios.post(
          'https://vue-todo-crud-default-rtdb.firebaseio.com/todos.json',
          item
        );
      })();
      this.todos.push(item);
      this.todoText = '';
    },
    fetchTodos() {
      axios(
        'https://vue-todo-crud-default-rtdb.firebaseio.com/todos.json'
      ).then((resp) => {
        for (let id in resp.data) {
          this.todos.push({
            id,
            isOpen: resp.data[id].isOpen,
            text: resp.data[id].text,
          });
        }
      });
    },
  },
  mounted() {
    this.fetchTodos();
  },
};
</script>

<style scoped>
.container {
  margin-top: 1rem;
}
.add-todo {
  display: flex;
  justify-content: center;
}
.add-todo span {
  font-size: 18px;
}
.add-todo input {
  margin: 0 20px;
  width: 200px;
  padding: 5px;
}
.add-todo button {
  height: 30px;
  background-color: '#e7e7e7';
}
.todo-list {
  margin-top: 20px;
  border: 1px solid #e7e7e7;
  box-shadow: 5px 5px 5px #d7d7d7;
  border-radius: 10px;
  padding: 10px;
  width: 400px;
}
</style>