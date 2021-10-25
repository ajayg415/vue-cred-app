<template>
  <li :class="{ checked: !localItem.isOpen }">
    <input
      type="checkbox"
      :id="localItem.id"
      :checked="!localItem.isOpen"
      @click="statusUpdated"
    />
    <label :for="item.id">{{ localItem.text }}</label>
  </li>
</template>

<script>
import axios from 'axios';

export default {
  props: ['item'],
  data() {
    return {
      localItem: { ...this.item },
    };
  },
  methods: {
    statusUpdated(el) {
      this.localItem.isOpen = el.target.checked;
      this.updateDB({
        id: this.item.id,
        isOpen: el.target.checked,
        text: this.item.text,
      });
    },
    updateDB(obj) {
      console.log(obj);
      axios
        .put(
          'https://vue-todo-crud-default-rtdb.firebaseio.com/todos.json/' +
            this.item.id +
            '/',
          obj
        )
        .then((res) => {
          console.log(res);
        });
    },
  },
};
</script>

<style scoped>
li {
  list-style: none;
  margin-top: 10px;
  text-transform: capitalize;
  border-bottom: 1px solid #d7d7d7;
  padding-bottom: 5px;
  font-size: 1.1rem;
}
li.checked {
  text-decoration: line-through;
}
li:last-of-type {
  border-bottom-width: 0;
}
li input {
  margin-right: 10px;
}
</style>