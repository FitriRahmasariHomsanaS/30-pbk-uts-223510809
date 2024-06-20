<template>
  <div class="about-container">
    <div class="about-content">
      <h1 class="about-title">Tentang Web Ini</h1>
      <p class="about-description">
        Website ini dirancang untuk memberikan pengalaman yang menyenangkan dan informatif bagi penggunanya. Kami fokus pada keindahan visual serta kemudahan navigasi.
      </p>
      <div class="features">
        <h3>Fitur Unggulan:</h3>
        <ul>
          <li>Desain Responsif</li>
          <li>Animasi Menarik</li>
          <li>Konten Berkualitas</li>
        </ul>
      </div>
      <button class="home-button" @click="goHome">Kembali ke Beranda</button>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    goHome() {
      this.$router.push('/');
    }
  }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap');

.about-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  padding: 20px;
}

.about-content {
  text-align: center;
  background: rgba(255, 255, 255, 0.5); 
  padding: 40px;
  border-radius: 20px;
  box-shadow: 0 0 20px rgba(156, 150, 150, 0.1);
  animation: fadeIn 2s ease-in-out;
  max-width: 600px;
  width: 100%; 
}

.about-title {
  font-size: 3rem;
  font-weight: 600;
  color: #4a148c;
  margin-bottom: 20px;
  text-shadow: 2px 2px 8px rgba(0, 0, 0, 0.1);
  animation: slideIn 1s ease-out;
  font-family: 'Poppins', sans-serif;
}

.about-description {
  font-size: 1.5rem;
  color: #333;
  margin-bottom: 30px;
  animation: fadeInUp 1.5s ease-in-out;
  font-family: 'Poppins', sans-serif;
}

.features {
  margin-top: 30px;
}

.features h3 {
  font-size: 1.8rem;
  color: #4a148c;
  margin-bottom: 10px;
  font-family: 'Poppins', sans-serif;
}

.features ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
  font-size: 1.2rem;
  color: #333;
  font-family: 'Poppins', sans-serif;
}

.home-button {
  padding: 12px 24px; 
  font-size: 1.2rem;
  color: #fff;
  background-color: #5e35b1;
  border: none;
  border-radius: 50px;
  cursor: pointer;
  transition: background-color 0.3s, transform 0.3s;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
  font-family: 'Poppins', sans-serif;
  display: inline-block; 
}

.home-button:hover {
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
