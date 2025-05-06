<script setup>
import { ref, computed, watch } from 'vue'
import TodoForm from './components/TodoForm.vue'
import TodoItem from './components/TodoItem.vue'

const todos = ref(JSON.parse(localStorage.getItem('todos')) || [])
const filter = ref('Semua')
const filters = ['Semua', 'Selesai', 'Belum selesai']

const addTodo = (text) => todos.value.push({ text, done: false })
const toggleTodo = (i) => todos.value[i].done = !todos.value[i].done
const deleteTodo = (i) => todos.value.splice(i, 1)

const filteredTodos = computed(() => {
  if (filter.value === 'Selesai') return todos.value.filter(t => t.done)
  if (filter.value === 'Belum selesai') return todos.value.filter(t => !t.done)
  return todos.value
})

watch(todos, () => {
  localStorage.setItem('todos', JSON.stringify(todos.value))
}, { deep: true })
</script>

<template>
<div class="container py-5">
<div class="card shadow-lg">
  <div class="card-body">
    <h1 class="text-center mb-4 text-primary">📝 To-Do List</h1>
    <TodoForm @add-todo="addTodo" />


    <div class="d-flex justify-content-center gap-2 my-3">
      <button
        v-for="f in filters"
        :key="f"
        class="btn"
        :class="filter === f ? 'btn-primary' : 'btn-outline-primary'"
        @click="filter = f"
      >
        {{ f }}
      </button>
    </div>


    <div v-if="filteredTodos.length">
      <TodoItem
        v-for="(todo, i) in filteredTodos"
        :key="i"
        :todo="todo"
        @toggle="toggleTodo(i)"
        @delete="deleteTodo(i)"
      />
    </div>
    <div v-else class="text-center text-muted">Tidak ada tugas.</div>
  </div>
</div>
</div>
</template>




<style>


</style>

