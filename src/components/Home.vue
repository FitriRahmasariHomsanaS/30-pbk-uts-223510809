<template>
  <div class="home-container">
    <div class="home-box">
      <div class="home-content">
        <div class="content-wrapper">
          <h1 class="home-title">TENTANG WEB</h1>
          <p class="home-description">Jelajahi Keunikan Web Ini</p>
          <router-link to="/about" class="btn" @click="handleAboutClick">Lebih Lanjut</router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    handleAboutClick() {
      this.$router.push('/about');
    }
  }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap');

.home-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  padding: 20px;
}

.home-box {
  background: rgba(255, 255, 255, 0.5); 
  border-radius: 20px;
  box-shadow: 0 0 20px rgba(218, 15, 15, 0.1);
  animation: fadeIn 2s ease-in-out;
  max-width: 600px; 
  width: 100%; 
}

.home-content {
  text-align: center;
  padding: 40px;
}

.content-wrapper {
  position: relative;
}

.home-title {
  font-size: 3rem;
  font-weight: 600;
  color: #4a148c;
  margin-bottom: 20px;
  text-shadow: 2px 2px 8px rgba(189, 181, 181, 0.87);
  animation: slideIn 1s ease-out;
  font-family: 'Poppins', sans-serif;
}

.home-description {
  font-size: 1.5rem;
  color: #333;
  margin-bottom: 30px;
  animation: fadeInUp 1.5s ease-in-out;
  font-family: 'Poppins', sans-serif;
}

.btn {
  padding: 12px 24px; 
  background-color: #5e35b1;
  color: #fff;
  text-decoration: none;
  border-radius: 50px;
  transition: background-color 0.3s, transform 0.3s;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
  font-family: 'Poppins', sans-serif;
  display: inline-block; 
}

.btn:hover {
  background-color: #7e57c2;
  transform: scale(1.1);
}

@keyframes fadeIn {
  0% { opacity: 0; }
  100% { opacity: 1; }
}

@keyframes slideIn {
  0% { transform: translateY(-20px); opacity: 0; }
  100% { transform: translateY(0); opacity: 1; }
}

@keyframes fadeInUp {
  0% { transform: translateY(20px); opacity: 0; }
  100% { transform: translateY(0); opacity: 1; }
}
</style>
