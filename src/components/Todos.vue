<template>
    <div>
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
  </template>
  
  <script>
  export default {
    data() {
      return {
        newActivity: {
          name: '',
          dateTime: ''
        },
        activities: [],
        showOnlyIncomplete: false
      };
    },
    computed: {
      filteredActivities() {
        if (this.showOnlyIncomplete) {
          return this.activities.filter(activity => !activity.completed);
        } else {
          return this.activities;
        }
      }
    },
    methods: {
      addActivity() {
        if (this.newActivity.name.trim() !== '' && this.newActivity.dateTime.trim() !== '') {
          this.activities.push({
            name: this.newActivity.name,
            dateTime: this.newActivity.dateTime,
            completed: false
          });
          this.newActivity.name = '';
          this.newActivity.dateTime = '';
        }
      },
      removeActivity(index) {
        this.activities.splice(index, 1);
      },
      editActivity(index) {
        if (confirm('Apakah Anda ingin mengedit kegiatan ini?')) {
          const newName = prompt('Masukkan nama kegiatan baru:', this.activities[index].name);
          const newDateTime = prompt('Masukkan tanggal & jam baru:', this.activities[index].dateTime);
          if (newName && newDateTime) {
            this.activities[index].name = newName;
            this.activities[index].dateTime = newDateTime;
          }
        }
      },
      formatDate(dateTime) {
        const options = { year: 'numeric', month: 'short', day: 'numeric', hour: 'numeric', minute: 'numeric' };
        return new Date(dateTime).toLocaleDateString('en-US', options);
      }
    }
  };
  </script>
  
  <style scoped>
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
    background-color: #a262b6;
    color: #fff;
    cursor: pointer;
  }
  button:hover {
    background-color: #020202;
  }
  table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 20px;
  }
  th, td {
    padding: 15px;
    border-bottom: 1px solid #dee2e6;
    text-align: left;
  }
  th {
    background-color: #f2f2f2;
  }
  tr:hover {
    background-color: #f5f5f5;
  }
  .filter-container {
    margin-top: 10px;
  }
  </style>
  