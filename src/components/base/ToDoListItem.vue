<template>
  <li>{{ item.text }}</li>
</template>

<script>
export default {
  props: ['item'],
};
</script>

<style scoped>
li {
  list-style: none;
  margin-top: 10px;
  text-transform: capitalize;
  border-bottom: 1px solid #d7d7d7;
  padding-bottom: 2px;
  font-size: 1.1rem;
}
</style>