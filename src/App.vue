<script setup>
import { ref } from "vue";

// 建立待辦事項的變數
const todos = ref([]);
const newTodo = ref("");

// 新增待辦事項
const addTodo = () => {
  if (newTodo.value.trim() !== "") {
    todos.value.push({ text: newTodo.value, done: false });
    newTodo.value = ""; // 清空輸入框
  }
};

// 刪除待辦事項
// splice(刪除索引, 數量)

const removeTodo = (index) => {
  todos.value.splice(index, 1);
};
</script>

<template>
  <div class="container">
    <h1>✅ Vue 3 待辦事項</h1>
    
    <div class="input-group">
      <input v-model="newTodo" placeholder="請輸入待辦事項..." />
      <button @click="addTodo">新增</button>
    </div>

    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        <span :class="{ done: todo.done }" @click="todo.done = !todo.done">
          {{ todo.text }}
        </span>
        <button @click="removeTodo(index)">❌</button>
      </li>
    </ul>
    <p v-if="todos.length === 0">目前沒有待辦事項</p>
  </div>
</template>

<style scoped>
.container {
  max-width: 400px;
  margin: auto;
  text-align: center;
  font-family: Arial, sans-serif;
}

.input-group {
  display: flex;
  gap: 8px;
  margin-bottom: 10px;
}

input {
  flex: 1;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

button {
  padding: 8px 12px;
  background-color: #42b983;
  color: white;
  border: none;
  cursor: pointer;
  border-radius: 5px;
}

button:hover {
  background-color: #36976a;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  display: flex;
  justify-content: space-between;
  padding: 8px;
  border-bottom: 1px solid #ddd;
}

.done {
  text-decoration: line-through;
  color: #999;
  cursor: pointer;
}
</style>

