<template>
  <q-page class="q-pa-md max-w-sm mx-auto">
    <h5 class="text-primary q-mt-none q-mb-md text-weight-regular">Todo List with Priority</h5>

    <TodoForm @submit-todo="appendTask" />

    <div
      class="row q-col-gutter-none border-primary rounded-borders overflow-hidden"
      style="border: 1px solid #1976d2"
    >
      <q-btn
        class="col-4"
        :class="activeFilter === 'all' ? 'bg-primary text-white' : 'bg-white text-primary'"
        label="ทั้งหมด"
        flat
        @click="activeFilter = 'all'"
      />
      <q-btn
        class="col-4"
        :class="activeFilter === 'pending' ? 'bg-warning text-white' : 'bg-white text-warning'"
        label="ยังไม่เสร็จ"
        flat
        @click="activeFilter = 'pending'"
      />
      <q-btn
        class="col-4"
        :class="activeFilter === 'done' ? 'bg-positive text-white' : 'bg-white text-positive'"
        label="เสร็จแล้ว"
        flat
        @click="activeFilter = 'done'"
      />
    </div>

    <TodoList :dataList="filteredTasks" @toggle-task="toggleTaskStatus" />
  </q-page>
</template>

<script setup>
import { ref, computed } from 'vue'
import TodoForm from './TodoForm.vue'
import TodoList from './TodoList.vue'

const todos = ref([])

const activeFilter = ref('all')

const appendTask = (newTask) => {
  todos.value.push(newTask)
}

const toggleTaskStatus = (taskId) => {
  const taskRef = todos.value.find((t) => t.id === taskId)
  if (taskRef) {
    taskRef.isDone = !taskRef.isDone
  }
}

const filteredTasks = computed(() => {
  if (activeFilter.value === 'done') {
    return todos.value.filter((t) => t.isDone)
  }
  if (activeFilter.value === 'pending') {
    return todos.value.filter((t) => !t.isDone)
  }
  return todos.value
})
</script>
