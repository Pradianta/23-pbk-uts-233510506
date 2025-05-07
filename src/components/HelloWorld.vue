<script setup>
import { ref, computed } from 'vue'

const activities = ref([
  { name: 'olahraga', completed: false },
  { name: 'makan', completed: false },
  { name: 'tidur', completed: false }
])
const newActivity = ref('')
const showUndoneOnly = ref(false)

const filteredActivities = computed(() => {
  if (showUndoneOnly.value) {
    return activities.value.filter(activity => !activity.completed)
  }
  return activities.value
})

const undoneCount = computed(() => activities.value.filter(activity => !activity.completed).length)

function addActivity() {
  if (newActivity.value.trim() !== '') {
    activities.value.push({ name: newActivity.value.trim(), completed: false })
    newActivity.value = ''
  }
}

function removeActivity(index) {
  activities.value.splice(index, 1)
}

function toggleShowUndone() {
  showUndoneOnly.value = !showUndoneOnly.value
}
</script>

<template>
  <div>
    <label for="activityInput">Daftar Kegiatan:</label>
    <input id="activityInput" type="text" v-model="newActivity" placeholder="Masukkan kegiatan" />
    <button type="button" @click="addActivity">Submit</button>
    <button type="button" @click="toggleShowUndone" style="margin-left: 10px;">Undone</button>
    <div style="margin-top: 10px;">Belum selesai: {{ undoneCount }}</div>

    <ul>
      <li v-for="(activity, index) in filteredActivities" :key="index">
        <input type="checkbox" v-model="activity.completed" />
        <span :style="{ textDecoration: activity.completed ? 'line-through' : 'none' }">{{ activity.name }}</span>
        <button type="button" @click="removeActivity(index)" style="margin-left: 10px;">Hapus</button>
      </li>
    </ul>
  </div>
</template>

<style scoped>

</style>
