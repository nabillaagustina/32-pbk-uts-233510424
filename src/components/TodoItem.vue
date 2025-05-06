<template>
  <div class="d-flex justify-content-between align-items-center border-bottom py-2">
    <div :class="{ 'text-decoration-line-through text-muted': todo.done }">
      {{ todo.text }}
    </div>
    <div class="d-flex gap-2 align-items-center">
      <input
        type="checkbox"
        :checked="todo.done"
        @change="$emit('toggle')"
        class="form-check-input"
      />
      <button class="btn btn-sm btn-danger" @click="$emit('delete')">🗑</button>
    </div>
  </div>
</template>


<script setup>
defineProps(['todo'])
</script>





