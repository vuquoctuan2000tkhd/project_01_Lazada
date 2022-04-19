<script setup>
import { ref, computed } from "vue";

let id = 0;

const newTodo = ref("");
const hideCompleted = ref(false);
const todos = ref([
  { id: id++, text: "Learn HTML", done: false },
  { id: id++, text: "Learn JavaScript", done:false },
  { id: id++, text: "Learn Vue", done: false },
]);
const filteredTodos = computed(() => {
  if(hideCompleted.value){return todos.value.filter((x) => !x.done)} else{ return todos.value;}
});
function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false });
  newTodo.value = "";
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo);
}
</script>

<template>
  
    <input v-model="newTodo" />
    <button @click="addTodo">Add Todo</button>
  
  <ul>
    <li v-for="todo in filteredTodos" :key="todo.id">
      <input type="checkbox" v-model="todo.done" />
      {{ todo.text }}
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
  <button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted?'show all':'Hide' }}
  </button>
</template>

