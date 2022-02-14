<script setup>
  import useTodos from '../composables/useTodos';

  const { pending, completed, changeStatus } = useTodos();

  defineProps({
    isCompleted: {
      default: false,
      type: Boolean,
    },
  });
</script>

<template>
  <div class="w-1/3">
    <h3
      class="text-2xl text-center"
      :class="isCompleted ? 'text-rose-600' : 'text-amber-600'"
    >
      {{ isCompleted ? 'Completed' : 'Pending' }}
    </h3>
    <ul class="pt-8 space-y-4">
      <li
        v-for="todo in isCompleted ? completed : pending"
        :key="todo.id"
        @click="changeStatus(todo.id)"
        :class="
          isCompleted
            ? 'text-rose-600 hover:bg-rose-400'
            : 'text-amber-600 hover:bg-amber-700'
        "
        class="
          w-full
          px-4
          py-2
          font-bold
          text-center
          transition-colors
          duration-500
          bg-gray-300
          rounded-lg
          hover:cursor-pointer hover:text-gray-200
        "
      >
        {{ todo.content }}
      </li>
    </ul>
  </div>
</template>