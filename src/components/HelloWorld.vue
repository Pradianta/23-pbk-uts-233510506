<script setup>
import { ref } from 'vue'

const activities = ref(['olahraga', 'makan', 'tidur'])
const newActivity = ref('')

function addActivity() {
  if (newActivity.value.trim() !== '') {
    activities.value.push(newActivity.value.trim())
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
        {{ activity }}
        <button type="button" @click="removeActivity(index)" style="margin-left: 10px;">x</button>
      </li>
    </ul>
  </div>
</template>

<style scoped>

</style>
