<script setup>
import { ref, computed } from "vue";

const newTodo = ref("");

const todos = ref([]);

const pending = computed(() => {
  return todos.value.filter((todo) => !todo.done);
});

const completed = computed(() => {
  return todos.value.filter((todo) => todo.done);
});

const addTodo = () => {
  if (newTodo.value.trim()) {
    todos.value.push({
      id: todos.value.length,
      content: newTodo.value,
      done: false,
    });
    newTodo.value = "";
  }
};

const changeStatus = (id) => {
  const todo = todos.value.find((todo) => todo.id === id);
  todo.done = !todo.done;
};
</script>

<template>
  <div class="min-h-screen bg-indigo-800">
    <div class="container flex flex-col pt-8 mx-auto space-y-8">
      <h1
        class="pb-4 text-6xl font-thin tracking-tight text-center text-purple-400"
      >
        🚀 My To do App
      </h1>
      <input
        @change="addTodo"
        v-model="newTodo"
        type="text"
        class="px-4 py-2 text-xl text-center rounded-lg"
        placeholder="New Entry"
      />
      <div class="flex justify-around">
        <div class="w-1/3">
          <h3 class="text-2xl text-center text-amber-600">Pending</h3>
          <ul class="pt-8 space-y-4">
            <li
              v-for="todo in pending"
              :key="todo.id"
              @click="changeStatus(todo.id)"
              class="w-full px-4 py-2 font-bold text-center text-amber-600 transition-colors duration-500 bg-gray-300 rounded-lg  hover:cursor-pointer hover:bg-amber-600 hover:text-gray-200"
            >
              {{ todo.content }}
            </li>
          </ul>
        </div>
        <div class="w-1/3">
          <h3 class="text-2xl text-center text-rose-600">Completed</h3>
          <ul class="pt-8 space-y-4">
            <li
              v-for="todo in completed"
              :key="todo.id"
              @click="changeStatus(todo.id)"
              class="w-full px-4 py-2 font-bold text-center text-rose-600 transition-colors duration-500 bg-gray-300 rounded-lg  hover:cursor-pointer hover:bg-rose-700 hover:text-gray-200"
            >
              {{ todo.content }}
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>


