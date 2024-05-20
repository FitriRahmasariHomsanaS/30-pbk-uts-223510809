<template>
    <div>
      <h1>Form List Kegiatan</h1>
      <div>
        <label for="activityName">Nama Kegiatan:</label> 
      </div>
      <input type="text" v-model="newActivity.name" placeholder="Tambahkan kegiatan baru">
      <div class="datetime-container">
        <label for="datetime">Tanggal & Jam:</label>
        <input id="datetime" type="datetime-local" v-model="newActivity.dateTime"> 
      </div>
      <button @click="addActivity">Tambah</button> <br>
  
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
          <tr v-for="(activity, index) in activities" :key="index">
            <td>{{ activity.name }}</td>
            <td>{{ formatDate(activity.dateTime) }}</td>
            <td>
              <input type="checkbox" v-model="activity.completed">
              <span :class="{ 'completed': activity.completed }">{{ activity.completed ? 'Selesai' : 'Belum Selesai' }}</span>
            </td>
            <td>
              <button @click="removeActivity(index)">Hapus</button>
              <button @click="editActivity(index)">Edit</button>
            </td>
          </tr>
        </tbody>
      </table>
  
      <!-- Slot for additional content -->
      <slot></slot>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      // Define props using defineProps if needed
    },
    setup() {
      // Define props using defineProps if needed
  
      const newActivity = {
        name: '',
        dateTime: ''
      };
      const activities = [];
      // Methods and other logic
  
      return {
        newActivity,
        activities,
        // Return methods and other values
      };
    }
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
  </style>
  