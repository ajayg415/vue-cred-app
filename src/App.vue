<template>
  <TheHeader title="Todo Sample CRUD Application" />
  <ToDoList />
</template>

<script>
import TheHeader from './components/ui/TheHeader.vue';
import ToDoList from './components/base/ToDoList.vue';

export default {
  components: {
    TheHeader,
    ToDoList,
  },
};
</script>
