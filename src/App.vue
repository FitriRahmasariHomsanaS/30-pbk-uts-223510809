<template>
  <div class="container">
    <header class="header">
      <nav class="menu">
        <ul>
          <li><router-link to="/">Home</router-link></li>
          <li><router-link to="/todos">Todos</router-link></li>
          <li><router-link to="/posts">Posts</router-link></li>
          <li><router-link to="/albums">Albums</router-link></li>
          <li><router-link to="/about">About</router-link></li>
        </ul>
      </nav>
    </header>
    <main class="main-content">
      <router-view></router-view>
    </main>
    <footer class="footer">
      <p>© 2024 Web ini dirancang untuk memberikan pengalaman yang menyenangkan dan informatif.</p>
    </footer>
  </div>
</template>

<script>
import Todos from './components/TodoList.vue';
import Posts from './components/PostList.vue';
import Albums from './components/AlbumList.vue';

export default {
  components: {
    Todos,
    Posts,
    Albums
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap');

body {
  font-family: 'Poppins', sans-serif;
  margin: 0;
  padding: 0;
  background: url('https://w0.peakpx.com/wallpaper/797/647/HD-wallpaper-purple-background-design-vector-art-icon-and-graphics-for-modern-purple.jpg');
  color: #000000;
}

.container {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

.header {
  width: 100%;
  background-color: rgba(191, 167, 201, 0.95);
  box-shadow: 0px 0px 20px rgba(0, 0, 0, 0.2);
  padding: 10px 0;
  margin-bottom: 20px;
}

.menu ul {
  display: flex;
  justify-content: center;
  list-style: none;
  padding: 0;
  margin: 0;
}

.menu li {
  margin: 0 15px;
}

.menu a {
  text-decoration: none;
  color: #fff;
  padding: 10px 20px;
  background-color: hwb(0 0% 100%);
  border-radius: 6px;
  transition: background-color 0.3s, box-shadow 0.3s;
  font-size: 1.5rem; /* Increase the font size */
}

.menu a:hover {
  background-color: #9e68d3;
  box-shadow: 0px 0px 10px rgba(255, 255, 255, 0.5);
}

.main-content {
  flex-grow: 1;
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
  box-sizing: border-box;
  background-color: rgba(255, 255, 255, 0.219);
  border-radius: 10px;
  box-shadow: 0px 0px 20px rgba(0, 0, 0, 0.5);
}

.footer {
  width: 100%;
  background-color: rgba(191, 167, 201, 0.95);
  text-align: center;
  padding: 10px 0;
  box-shadow: 0px 0px 20px rgba(0, 0, 0, 0.2);
  margin-top: 20px;
}

.router-link-active {
  background-color: #4b2c5e;
}
</style>
