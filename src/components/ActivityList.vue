<template>
  <div>
    <h1>Header</h1>
    <nav>
      <ul>
        <li>
          <button @click="selectedComponent = 'todos'" class="btn btn-primary" style="color: violet; font-weight: bold;">Todos</button>
        </li>
        <li>
          <button @click="selectedComponent = 'post'" class="btn btn-primary" style="color: violet; font-weight: bold;">Post</button>
        </li>
      </ul>
    </nav>

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
      <button @click="addActivity">Tambah</button> <br>
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
            <td><button @click="removeActivity(index)">Hapus</button></td>
          </tr>
        </tbody>
      </table>
    </div>

    <div v-else-if="selectedComponent === 'post'">
      <h1>Posts</h1>
      <form @submit.prevent="getPosts">
        <label for="userId">Pilih Pengguna:</label>
        <select v-model="selectedUserId" id="userId" class="form-control user-select">
          <option v-for="user in users" :value="user.id" :key="user.id">{{ user.name }}</option>
        </select>
        <button class="btn btn-primary tombol" type="submit">Dapatkan Posting</button>
      </form>
      <div v-if="loading">Loading...</div>
      <div v-else>
        <div v-for="post in posts" :key="post.id">
          <strong>User ID:</strong> {{ post.userId }}<br>
          <strong>ID:</strong> {{ post.id }}<br>
          <strong>Title:</strong> {{ post.title }}<br>
          <strong>Body:</strong> {{ post.body }}<br><br>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selectedComponent: 'todos',
      newActivity: {
        name: '',
        dateTime: ''
      },
      activities: [],
      selectedUserId: '',
      users: [],
      loading: false,
      posts: []
    };
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
    formatDate(dateTime) {
      const options = { year: 'numeric', month: 'short', day: 'numeric', hour: 'numeric', minute: 'numeric' };
      return new Date(dateTime).toLocaleDateString('en-US', options);
    },
    getPosts() {
      this.loading = true;
      fetch(`https://jsonplaceholder.typicode.com/posts?userId=${this.selectedUserId}`)
        .then(response => response.json())
        .then(data => {
          this.posts = data;
          this.loading = false;
        })
        .catch(error => {
          console.error('Error fetching posts:', error);
          this.loading = false;
        });
    }
  },
  mounted() {
    // Fetch list of users
    fetch('https://jsonplaceholder.typicode.com/users')
      .then(response => response.json())
      .then(data => {
        this.users = data;
      })
      .catch(error => {
        console.error('Error fetching users:', error);
      });
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
.user-select {
  margin-bottom: 10px;
}
</style>
