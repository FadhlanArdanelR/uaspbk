<template>
  <div class="home-container">
    <div class="home-overlay"></div>
    <div class="home-content">
      <h1 class="home-title">Eksplorasi Dunia Bersama Kami</h1>
      <p class="home-description">Temukan Keindahan Dunia dengan Berbagai Konten Menarik, Mulai dari Pencatatan Tugas Harian, Cerita Tentang Kegiatan Anda, hingga Galeri Foto yang Mengagumkan.</p>
      <router-link to="/about" class="btn" @click="handleAboutClick">Tentang Kami</router-link>
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
}
</script>

<style>
.home-container {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-image: url(https://png.pngtree.com/thumb_back/fh260/background/20231230/pngtree-elegant-gold-accented-black-abstract-background-texture-image_13886480.png);
  background-size: cover;
  background-position: center;
}

.home-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5); /* Ubah nilai alpha untuk mengatur transparansi overlay */
}

.home-content {
  text-align: center;
  z-index: 2;
  color: #fff;
  max-width: 600px;
  padding: 20px;
}

.home-title {
  font-size: 48px;
  font-weight: bold;
  margin-bottom: 20px;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
}

.home-description {
  font-size: 20px;
  margin-bottom: 30px;
  line-height: 1.6;
}

.btn {
  display: inline-block;
  padding: 12px 24px;
  background-color: #ff6600;
  color: #fff;
  text-decoration: none;
  border-radius: 5px;
  transition: background-color 0.3s;
  font-weight: bold;
}

.btn:hover {
  background-color: #e65c00;
}
</style>
