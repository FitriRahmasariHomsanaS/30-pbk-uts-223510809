<template>
  <div>
    <label for="userSelect">Pilih Pengguna:</label>
    <select id="userSelect" v-model="selectedUser" @change="fetchPosts">
      <option v-for="user in users" :key="user.id" :value="user.id">{{ user.name }}</option>
    </select>

    <div v-if="posts.length" class="posts-container">
      <h2 class="post-heading">Postingan oleh {{ getUserName(selectedUser) }}</h2>
      <ul>
        <li v-for="post in posts" :key="post.id" class="post-item">
          <h3>{{ post.title }}</h3>
          <p>{{ post.body }}</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import { defineProps } from 'vue';

export default {
  data() {
    return {
      users: [],
      selectedUser: null,
      posts: []
    };
  },
  methods: {
    fetchUsers() {
      fetch('https://jsonplaceholder.typicode.com/users')
        .then(response => response.json())
        .then(data => {
          this.users = data;
        })
        .catch(error => console.error('Error fetching users:', error));
    },
    fetchPosts() {
      if (this.selectedUser) {
        fetch(`https://jsonplaceholder.typicode.com/posts?userId=${this.selectedUser}`)
          .then(response => response.json())
          .then(data => {
            this.posts = data;
          })
          .catch(error => console.error('Error fetching posts:', error));
      }
    },
    getUserName(userId) {
      const user = this.users.find(user => user.id === userId);
      return user ? user.name : 'Pengguna Tidak Dikenal';
    }
  },
  mounted() {
    this.fetchUsers();
  }
};
</script>

<style scoped>
select {
  padding: 12px;
  margin-bottom: 15px;
  border: none;
  border-radius: 6px;
  font-size: 15px;
  background-color: rgba(255, 255, 255, 0.95);
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  transition: background-color 0.3s, box-shadow 0.3s;
  outline: none;
}

select:focus {
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.3);
}

ul {
  list-style-type: none;
  padding: 0;
}

.posts-container {
  margin-top: 20px;
}

.post-heading {
  font-size: 23px;
  margin-bottom: 15px;
  color: #4a148c;
}

.post-item {
  background-color: rgba(255, 255, 255, 0.95);
  margin-bottom: 10px;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  transition: background-color 0.3s, box-shadow 0.3s;
}

.post-item:hover {
  background-color: #f5f5f5;
}

h3 {
  margin: 0 0 10px;
  font-size: 20px;
  color: #6a1b9a;
}

p {
  margin: 0;
  color: #333;
}
</style>
