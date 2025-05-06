<template>
  <form @submit.prevent="submitTodo" class="input-group mb-3">
    <input
      v-model="text"
      class="form-control"
      placeholder="Tambahkan tugas baru..."
    />
    <button class="btn btn-success" type="submit">Tambah</button>
  </form>
</template>


<script setup>
import { ref } from 'vue'
const text = ref('')
const emit = defineEmits(['add-todo'])


const submitTodo = () => {
  if (text.value.trim()) {
    emit('add-todo', text.value)
    text.value = ''
  }
}
</script>



