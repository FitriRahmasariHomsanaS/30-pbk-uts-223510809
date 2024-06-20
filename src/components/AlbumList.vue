<template>
  <div class="album-container">
    <h2 class="title">Albums</h2>
    <div v-if="albums.length">
      <table class="album-table">
        <tbody>
          <tr v-for="album in albums" :key="album.id" @click="viewAlbum(album.id)" class="album-item">
            <td class="album-id">{{ album.id }}</td>
            <td class="album-title">{{ album.title }}</td>
          </tr>
        </tbody>
      </table>
    </div>
    <div v-else class="no-albums">
      <p>No albums available.</p>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useAlbumsStore } from '../stores/albums';
import { useRouter } from 'vue-router';

const albumsStore = useAlbumsStore();
const albums = ref([]);
const router = useRouter();

const fetchAlbums = async () => {
  await albumsStore.fetchAlbums();
  albums.value = albumsStore.albums;
};

const viewAlbum = (id) => {
  router.push(`/albums/${id}`);
};

onMounted(fetchAlbums);
</script>

<style scoped>
.album-container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  background: rgba(255, 255, 255, 0.9);
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
  border-radius: 10px;
}

.title {
  color: #007bff;
  text-align: center;
  font-weight: bold;
  font-size: 24px;
  margin-bottom: 20px;
}

.album-table {
  width: 100%;
  border-collapse: separate;
  border-spacing: 0 10px;
}

.album-item {
  transition: background-color 0.3s, color 0.3s;
  cursor: pointer;
  background: rgba(240, 240, 240, 0.8);
  border-radius: 5px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.album-item:hover {
  background-color: #007bff;
  color: white;
}

.album-id, .album-title {
  padding: 10px;
  border: 1px solid #007bff;
}

.album-id {
  font-weight: bold;
}

.album-title {
  font-family: 'Arial', sans-serif;
}

.no-albums {
  text-align: center;
  margin-top: 20px;
  font-size: 18px;
  color: #666;
}
</style>
