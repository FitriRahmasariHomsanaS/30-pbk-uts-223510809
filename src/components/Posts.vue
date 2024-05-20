<template>
    <div>
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
  
      const selectedUserId = ref('');
      const users = ref([]);
      const loading = ref(false);
      const posts = ref([]);
  
      const getPosts = () => {
        loading.value = true;
        fetch(`https://jsonplaceholder.typicode.com/posts?userId=${selectedUserId.value}`)
          .then(response => response.json())
          .then(data => {
            posts.value = data;
            loading.value = false;
          })
          .catch(error => {
            console.error('Error fetching posts:', error);
            loading.value = false;
          });
      };
  
      // Fetch list of users
      fetch('https://jsonplaceholder.typicode.com/users')
        .then(response => response.json())
        .then(data => {
          users.value = data;
        })
        .catch(error => {
          console.error('Error fetching users:', error);
        });
  
      return {
        selectedUserId,
        users,
        loading,
        posts,
        getPosts
      };
    }
  };
  </script>
  
  <style>
  .user-select {
    margin-bottom: 10px;
  }
  </style>
  