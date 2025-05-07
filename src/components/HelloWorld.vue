<script setup>
import { ref } from 'vue'

const activities = ref([
  { name: 'olahraga', completed: false },
  { name: 'makan', completed: false },
  { name: 'tidur', completed: false }
])
const newActivity = ref('')

function addActivity() {
  if (newActivity.value.trim() !== '') {
    activities.value.push({ name: newActivity.value.trim(), completed: false })
    newActivity.value = ''
  }
}

function removeActivity(index) {
  activities.value.splice(index, 1)
}
</script>

<template>
  <div>
    <label for="activityInput">Daftar Kegiatan:</label>
    <input id="activityInput" type="text" v-model="newActivity" placeholder="Masukkan kegiatan" />
    <button type="button" @click="addActivity">Submit</button>

    <ul>
      <li v-for="(activity, index) in activities" :key="index">
        <input type="checkbox" v-model="activity.completed" />
        <span>{{ activity.name }}</span>
        <button type="button" @click="removeActivity(index)" style="margin-left: 10px;">Hapus</button>
      </li>
    </ul>
  </div>
</template>

<style scoped>

</style>
