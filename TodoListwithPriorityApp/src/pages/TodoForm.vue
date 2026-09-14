<template>
  <div class="q-pa-md bg-grey-1 rounded-borders q-mb-md">
    <q-input v-model="taskModel" label="สิ่งที่ต้องทำ" filled dense class="q-mb-sm" />

    <q-select
      v-model="priorityModel"
      :options="priorityOptions"
      label="ความสำคัญ"
      filled
      dense
      class="q-mb-md"
    />

    <div class="row q-gutter-sm">
      <q-btn color="primary" label="ADD" @click="emitTask" />
      <q-btn flat color="primary" label="RESET" @click="clearForm" />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const emit = defineEmits(['submit-todo'])

const taskModel = ref('')
const priorityModel = ref('Medium')
const priorityOptions = ['High', 'Medium', 'Low']

const emitTask = () => {
  if (!taskModel.value.trim()) return

  emit('submit-todo', {
    id: Date.now(),
    title: taskModel.value,
    level: priorityModel.value,
    isDone: false,
  })

  clearForm()
}

const clearForm = () => {
  taskModel.value = ''
  priorityModel.value = 'Medium'
}
</script>
