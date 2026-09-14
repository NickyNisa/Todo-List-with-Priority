<template>
  <q-list bordered class="rounded-borders q-mt-md overflow-hidden">
    <q-item v-for="task in dataList" :key="task.id" :class="getBgColor(task.level)" class="q-py-md">
      <q-item-section>
        <q-item-label :class="{ 'text-strike text-grey-5': task.isDone }">
          {{ task.title }}
        </q-item-label>
      </q-item-section>

      <q-item-section side>
        <q-item-label class="text-weight-bold text-black">
          {{ task.level }}
        </q-item-label>
      </q-item-section>

      <q-item-section side>
        <q-btn
          flat
          round
          dense
          :icon="task.isDone ? 'check' : ''"
          :color="task.isDone ? 'primary' : 'grey-4'"
          @click="$emit('toggle-task', task.id)"
        />
      </q-item-section>
    </q-item>

    <q-item v-if="dataList.length === 0" class="text-center text-grey-6 q-pa-md">
      <q-item-section>ไม่มีรายการในหมวดหมู่นี้</q-item-section>
    </q-item>
  </q-list>
</template>

<script setup>
defineProps({
  dataList: {
    type: Array,
    required: true,
  },
})

defineEmits(['toggle-task'])

const getBgColor = (level) => {
  if (level === 'High') return 'bg-red-1'
  if (level === 'Medium') return 'bg-orange-1'
  if (level === 'Low') return 'bg-green-1'
  return ''
}
</script>
