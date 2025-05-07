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
  <div class="container">
    <div class="header">
      <label for="activityInput" class="title">
        Daftar Kegiatan
      </label>
      <button type="button" @click="toggleShowUndone" class="undone-button">
        Undone: {{ undoneCount }}
      </button>
    </div>
    <div class="input-group">
      <input id="activityInput" type="text" v-model="newActivity" placeholder="Masukkan kegiatan" class="activity-input" />
      <button type="button" @click="addActivity" class="submit-button">
        Submit
      </button>
    </div>

    <ul class="activity-list">
      <li v-for="(activity, index) in filteredActivities" :key="index" class="activity-item">
        <input type="checkbox" v-model="activity.completed" />
        <span :class="{ completed: activity.completed }">{{ activity.name }}</span>
        <button type="button" @click="removeActivity(index)" class="delete-btn">Hapus</button>
      </li>
    </ul>

  </div>
</template>

<style scoped>
:global(body) {
  background: linear-gradient(135deg, #a1c4fd 0%, #c2e9fb 100%);
  min-height: 100vh;
  background-image: url(../assets/x.jpg);
  margin: 0;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.container {
  max-width: 420px;
  margin: 50px auto;
  padding: 30px 40px;
  background: linear-gradient(135deg, #06578d92 0%, #c3cfe2 100%);
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.15);
  border-radius: 20px;
  color: #222222;
  transition: box-shadow 0.3s ease;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.container:hover {
  box-shadow: 0 14px 35px rgba(0, 0, 0, 0.25);
}

.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.title {
  font-weight: 700;
  font-size: 1.4rem;
  color: #2c3e50;
  letter-spacing: 0.03em;
  margin: 0;
}

.undone-button {
  padding: 8px 18px;
  font-weight: 700;
  font-size: 1.1rem;
  border-radius: 12px;
  background-color: #2980b9;
  color: white;
  border: none;
  cursor: pointer;
  box-shadow: 0 5px 15px rgba(41, 128, 185, 0.7);
  transition: background-color 0.3s ease, box-shadow 0.3s ease, transform 0.2s ease;
}

.undone-button:hover {
  background-color: #1c5980;
  box-shadow: 0 7px 20px rgba(28, 89, 128, 0.9);
  transform: scale(1.05);
}

.input-group {
  display: flex;
  gap: 12px;
}

.activity-input {
  flex-grow: 1;
  padding: 14px 18px;
  font-size: 1.1rem;
  border: 2px solid #2980b9;
  border-radius: 12px;
  transition: border-color 0.3s ease, box-shadow 0.3s ease;
  box-sizing: border-box;
  color: #34495e;
  font-weight: 500;
}

.activity-input:focus {
  outline: none;
  border-color: #3498db;
  box-shadow: 0 0 10px rgba(52, 152, 219, 0.7);
}

.submit-button {
  padding: 14px 26px;
  font-size: 1.1rem;
  font-weight: 700;
  color: #ffffff;
  background-color: #2980b9;
  border: none;
  border-radius: 12px;
  cursor: pointer;
  box-shadow: 0 5px 15px rgba(41, 128, 185, 0.7);
  transition: background-color 0.3s ease, box-shadow 0.3s ease;
}

.submit-button:hover {
  background-color: #1c5980;
  box-shadow: 0 7px 20px rgba(28, 89, 128, 0.9);
}

.activity-list {
  list-style: none;
  padding-left: 0;
  margin: 0;
  max-height: 300px;
  overflow-y: auto;
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.activity-item {
  display: flex;
  align-items: center;
  padding: 12px 0;
  border-bottom: 1px solid #d1d8e0;
  transition: background-color 0.3s ease;
}

.activity-item:hover {
  background-color: #eaf2f8;
}

input[type="checkbox"] {
  width: 22px;
  height: 22px;
  margin-right: 16px;
  accent-color: #2980b9;
  cursor: pointer;
  transition: transform 0.2s ease;
}

input[type="checkbox"]:hover {
  transform: scale(1.1);
}

span {
  flex-grow: 1;
  font-size: 1.15rem;
  color: #2c3e50;
  user-select: none;
}

span.completed {
  color: #95a5a6;
  text-decoration: line-through;
}

button.delete-btn {
  background-color: #e74c3c;
  margin-left: 16px;
  padding: 8px 16px;
  font-size: 1rem;
  font-weight: 700;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(231, 76, 60, 0.7);
  transition: background-color 0.3s ease, box-shadow 0.3s ease;
}

button.delete-btn:hover {
  background-color: #c0392b;
  box-shadow: 0 6px 16px rgba(192, 57, 43, 0.9);
}
</style>
