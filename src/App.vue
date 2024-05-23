<template>
  <div class="container">
    <h1>Form List Kegiatan</h1>

    <div class="header">
      <button @click="currentView = 'todos'">Todos</button>
      <button @click="currentView = 'posts'">Posts</button>
    </div>

    <Todos v-if="currentView === 'todos'" />
    <Posts v-if="currentView === 'posts'" />
  </div>
</template>

<script>
import Todos from './components/Todos.vue';
import Posts from './components/Posts.vue';


export default {
  components: {
    Todos,
    Posts
  },
  data() {
    return {
      currentView: 'todos'
    };
  }
};
</script>

<style>
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
  background-color: rgba(191, 167, 201, 0.95);
  border-radius: 10px;
  box-shadow: 0px 0px 20px rgba(0, 0, 0, 0.2);
  padding: 30px;
  width: 80%;
  max-width: 600px;
  border: 1px solid rgba(0, 0, 0, 0.1);
}

h1 {
  color: rgb(0, 0, 0);
  text-align: center;
  margin-bottom: 20px;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
}

.header {
  display: flex;
  justify-content: space-around;
  margin-bottom: 20px;
}

.header button {
  padding: 10px 20px;
  font-size: 16px;
  background-color: #a262b6;
  color: #fff;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  transition: background-color 0.3s, box-shadow 0.3s;
}

.header button:hover {
  background-color: #020202;
}
</style>
