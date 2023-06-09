<template>
  <div>
    <div style="margin-top: 50px;">
      <div class="add-todo">
        <input type="text" v-model="newTodo" placeholder="Tambahkan todo baru" @keydown.enter="addTodo">
        <button @click="addTodo()">Tambah</button>
      </div>
      <div class="checkbox-list">
        <label v-for="(item, index) in itemList" :key="index" :class="{ 'selected': selectedItems.includes(item) }">
          <input type="checkbox" :value="item" :checked="isChecked(item)" @change="toggleItem(item)">
          <span style="margin-right: 10px;">{{ item }}</span>
          <button @click="deleteTodo(index)">Hapus</button>
        </label>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ListComponents',
  props: {
    itemList: {
      type: Array,
    },
  },
  data() {
    return {
      selectedItems: [],
      newTodo: ''
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== '') {
        this.$emit('itemAdded', this.newTodo);
        this.newTodo = '';
      }
    },

    deleteTodo(index) {
      this.$emit('itemDeleted', index);
    },

    toggleItem(item) {
      if (this.selectedItems.includes(item)) {
        this.selectedItems = this.selectedItems.filter(i => i !== item);
      } else {
        this.selectedItems.push(item);
      }
    },
    isChecked(item) {
      return this.selectedItems.includes(item);
    },
  },
}
</script>
<style>
.add-todo {
  display: flex;
  margin-top: 10px;
  justify-content: center;
}

.add-todo input {
  padding: 5px;
  width: 20%;
}

.add-todo button {
  margin-left: 10px;
}

label {
  display: flex;
  align-items: center;
  justify-content: center;
}

input {
  margin-right: 10px;
}
.checkbox-list {
  display: flex;
  flex-direction: column;
  margin-top: 15px;
}

.checkbox-list label {
  margin-bottom: 10px;
}

.checkbox-list label.selected {
  text-decoration: line-through;
}

.checkbox-list label.selected span {
  color: green;
}
</style>