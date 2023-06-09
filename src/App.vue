<template>
  <div>
    <div>Todo list</div>
    <ListComponents :itemList="items" @itemAdded="handleItemAdded" @itemDeleted="handleItemDeleted"></ListComponents>
  </div>
</template>

<script>
import ListComponents from './components/ListTodo.vue'
export default {
  name: 'App',
  data() {
    return {
      items: ['Berlari', 'Makan', 'Mandi', 'Tidur'],
    }
  },
  methods: {
    handleItemAdded(data) {
      this.items.push(data);
    },
    handleItemDeleted(index) {
      this.items.splice(index, 1);
    }
  },
  components: {
    ListComponents
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
