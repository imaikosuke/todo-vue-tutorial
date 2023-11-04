<template>
  <div class="todo-app">
    <h1>{{ appTitle }}</h1>
    <form @submit.prevent="addTodo" class="todo-form">
      <input
        type="text"
        v-model="newTodo"
        placeholder="新しいTodoを入力"
        class="todo-input"
        autofocus
      />
      <button type="submit" class="todo-add-btn">追加</button>
    </form>
    <ul class="todo-list">
      <li v-for="todo in todos" :key="todo.id" class="todo-item">
        {{ todo.text }}
        <button @click="removeTodo(todo.id)" class="todo-remove-btn">
          削除
        </button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const appTitle = 'Todoアプリ';
const newTodo = ref('');
const todos = ref([]);
const nextId = ref(1);

const addTodo = () => {
  if (newTodo.value.trim() === '') {
    return;
  }
  todos.value.push({ id: nextId.value, text: newTodo.value });
  nextId.value++;
  newTodo.value = '';
};

const removeTodo = (id) => {
  todos.value = todos.value.filter((todo) => todo.id !== id);
};
</script>

<style scoped>
.todo-app {
  max-width: 80%;
  margin: 0 auto;
  padding: 1em;
  background-color: #484848;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 128, 0, 0.1);
}

.todo-app h1 {
  color: white;
  text-align: center;
}

.todo-form {
  display: flex;
  gap: 0.5em;
  margin-bottom: 1em;
}

.todo-input {
  flex-grow: 1;
  padding: 0.5em;
  border-radius: 4px;
  outline-color: rgb(11, 3, 255);
}

.todo-add-btn {
  font-weight: bold;
  padding: 0.5em 1em;
  background-color: #10b981;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.todo-add-btn:hover {
  background-color: #059669;
}

.todo-list {
  list-style: none;
  padding: 0;
}

.todo-item {
  padding: 0.5em;
  margin-bottom: 0.5em;
  background-color: white;
  border-radius: 4px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.todo-remove-btn {
  font-weight: bold;
  padding: 0.3em 0.6em;
  background-color: #ef4444;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.todo-remove-btn:hover {
  background-color: #dc2626;
}
</style>
