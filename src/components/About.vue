<template>
  <div class="about-container">
    <div class="about-overlay"></div>
    <div class="about-content">
      <h1 class="about-title">Tentang Saya</h1>
      <p class="about-description">Saya kelahiran pekanbaru, tanggal 26 bulan 12 tahun 2003, saya suka bermain futsal bersama teman saya, saya suka makan nasi goreng raja minas</p>
    </div>
  </div>
</template>

<script>
export default {
  
}
</script>

<style scoped>
.about-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  position: relative;
  background-image: url('https://png.pngtree.com/thumb_back/fh260/background/20231230/pngtree-elegant-gold-accented-black-abstract-background-texture-image_13886480.png');
  background-size: cover;
  background-position: center;
  overflow: hidden; /* Mengatasi overflow pada gambar latar belakang */
}

.about-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.6); /* Overlay transparan untuk peningkatan kontras */
}

.about-content {
  text-align: center;
  z-index: 1; /* Mengatur konten agar muncul di atas latar belakang */
  color: #fff;
  max-width: 600px;
  padding: 20px;
}

.about-title {
  font-size: 48px;
  font-weight: bold;
  margin-bottom: 20px;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.8); /* Bayangan teks untuk meningkatkan kejelasan */
}

.about-description {
  font-size: 20px;
  line-height: 1.6;
  margin-bottom: 30px;
}

@media (max-width: 768px) {
  .about-title {
    font-size: 36px;
  }
}
</style>
