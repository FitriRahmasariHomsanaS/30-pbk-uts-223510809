<template>
  <div id="app">
    <div class="btn-container">
      <button @click="selectedComponent = 'todos'" :class="{ 'active': selectedComponent === 'todos' }" class="btn btn-primary">Todos</button>
      <button @click="selectedComponent = 'post'" :class="{ 'active': selectedComponent === 'post' }" class="btn btn-primary">Post</button>
    </div>

    <div class="component-container">
      <div v-if="selectedComponent === 'todos'">
        <h1>Form List Kegiatan</h1>
        <div>
          <label for="activityName">Nama Kegiatan:</label>
        </div>
        <input type="text" v-model="newActivity.name" placeholder="Tambahkan kegiatan baru">
        <div class="datetime-container">
          <label for="datetime">Tanggal & Jam:</label>
          <input id="datetime" type="datetime-local" v-model="newActivity.dateTime">
        </div>
        <button @click="addActivity">Tambah</button>

        <div class="filter-container">
          <input type="checkbox" v-model="showOnlyIncomplete"> Hanya Tampilkan Kegiatan Belum Selesai
        </div>

        <table>
          <thead>
            <tr>
              <th>Kegiatan</th>
              <th>Tanggal & Jam</th>
              <th>Status</th>
              <th>Aksi</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(activity, index) in filteredActivities" :key="index">
              <td>{{ activity.name }}</td>
              <td>{{ formatDate(activity.dateTime) }}</td>
              <td>
                <input type="checkbox" v-model="activity.completed">
                <span :class="{ 'completed': activity.completed }">{{ activity.completed ? 'Selesai' : 'Belum Selesai' }}</span>
              </td>
              <td>
                <button @click="editActivity(index)">Edit</button>
                <button @click="removeActivity(index)">Hapus</button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>

      <div v-else-if="selectedComponent === 'post'">
        <h1>Posts</h1>
        <ol>
          <li v-for="post in posts" :key="post.id">
            <strong>User ID:</strong> {{ post.userId }}<br>
            <strong>ID:</strong> {{ post.id }}<br>
            <strong>Title:</strong> {{ post.title }}<br>
            <strong>Body:</strong> {{ post.body }}<br><br>
          </li>
        </ol>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';

const selectedComponent = ref('todos');

const newActivity = {
  name: '',
  dateTime: ''
};

const editedActivity = {
  name: '',
  dateTime: ''
};

const activities = [];

const showOnlyIncomplete = ref(false);

const posts = ref([]);

const fetchPosts = () => {
  fetch('https://jsonplaceholder.typicode.com/posts')
    .then(response => response.json())
    .then(data => {
      posts.value = data;
    })
    .catch(error => {
      console.error('There was an error!', error);
    });
};

onMounted(() => {
  fetchPosts(); 
});

const filteredActivities = computed(() => {
  if (showOnlyIncomplete.value) {
    return activities.filter(activity => !activity.completed);
  } else {
    return activities;
  }
});

const addActivity = () => {
  if (newActivity.name.trim() !== '' && newActivity.dateTime.trim() !== '') {
    activities.push({ 
      name: newActivity.name, 
      dateTime: newActivity.dateTime, 
      completed: false 
    });
    newActivity.name = '';
    newActivity.dateTime = '';
  }
};

const removeActivity = (index) => {
  activities.splice(index, 1);
};

const editActivity = (index) => {
  editedActivity.name = activities[index].name;
  editedActivity.dateTime = activities[index].dateTime;
  if (confirm('Apakah Anda ingin mengedit kegiatan ini?')) {
    const newName = prompt('Masukkan nama kegiatan baru:', activities[index].name);
    const newDateTime = prompt('Masukkan tanggal & jam baru:', activities[index].dateTime);
    if (newName && newDateTime) {
      activities[index].name = newName;
      activities[index].dateTime = newDateTime;
    }
  }
};

const formatDate = (dateTime) => {
  const options = { year: 'numeric', month: 'short', day: 'numeric', hour: 'numeric', minute: 'numeric' };
  return new Date(dateTime).toLocaleDateString('en-US', options);
};
</script>

<style>
.completed {
  text-decoration: line-through;
}

.datetime-container {
  margin-top: 10px;
}

.datetime-container label {
  display: block;
  margin-bottom: 5px;
}

.btn-container {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}

.btn {
  color: violet;
  font-weight: bold;
  margin-right: 10px;
}

.active {
  background-color: violet;
  color: white;
}

.component-container {
  margin-top: 20px;
}

body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background: linear-gradient(to right bottom, rgb(160, 157, 161), rgb(140, 101, 155), rgb(135, 48, 161));
}

.container {
  background-color: rgba(255, 255, 255, 0.95);
  border-radius: 10px;
  box-shadow: 0px 0px 20px rgba(0, 0, 0, 0.2);
  padding: 30px;
  width: 80%;
  max-width: 600px;
  border: 1px solid rgba(0, 0, 0, 0.1);
}

h1 {
  color: black;
  text-align: center;
  margin-bottom: 20px;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
}

form {
  display: flex;
  flex-direction: column;
}

label {
  font-weight: bold;
  margin-bottom: 5px;
  color: #343c40;
}

input[type="text"],
input[type="date"],
button {
  padding: 12px;
  margin-bottom: 15px;
  border: none;
  border-radius: 6px;
  font-size: 16px;
  background-color: rgba(255, 255, 255, 0.95);
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  transition: background-color 0.3s, box-shadow 0.3s;
}

input[type="text"]:focus,
input[type="date"]:focus,
button:focus {
  outline: none;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.3);
}

button {
  background-color: #3c4bd9;
  color: #fff;
  cursor: pointer;
}

button:hover {
  background-color: #607386;
}
</style>
