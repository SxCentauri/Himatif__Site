<script setup>
</script>

<template>
  <div class="min-h-screen flex flex-col bg-gray-50">
    <!-- Navbar -->
    <header class="bg-white shadow">
      <div class="container mx-auto flex justify-between items-center p-4">
        <h1 class="text-xl font-bold text-indigo-600">HIMATIF</h1>
        <nav class="space-x-6">
          <a href="#about" class="text-gray-700 hover:text-indigo-600">Tentang</a>
          <a href="#activities" class="text-gray-700 hover:text-indigo-600">Kegiatan</a>
          <a href="#contact" class="text-gray-700 hover:text-indigo-600">Kontak</a>
        </nav>
      </div>
    </header>

    <!-- Hero Section -->
    <section class="bg-indigo-600 text-white text-center py-24">
      <h2 class="text-4xl font-bold">Selamat Datang di HIMATIF</h2>
      <p class="mt-4 text-lg">Himpunan Mahasiswa Teknik Informatika</p>
    </section>

    <!-- About Section -->
    <section id="about" class="container mx-auto py-16 px-4">
      <h3 class="text-2xl font-bold mb-6">Tentang Kami</h3>
      <p class="text-gray-700 leading-relaxed">
        HIMATIF merupakan organisasi mahasiswa yang bergerak di bidang teknologi informasi...
      </p>
    </section>

    <!-- Activities Section -->
    <section id="activities" class="bg-gray-100 py-16 px-4">
      <div class="container mx-auto">
        <h3 class="text-2xl font-bold mb-6">Kegiatan</h3>
        <div class="grid md:grid-cols-3 gap-6">
          <div class="bg-white p-6 rounded-xl shadow">
            <h4 class="font-bold text-lg mb-2">IT Mastery</h4>
            <p class="text-gray-600">Kegiatan seminar dan pelatihan IT terbaru.</p>
          </div>
          <div class="bg-white p-6 rounded-xl shadow">
            <h4 class="font-bold text-lg mb-2">Lomba</h4>
            <p class="text-gray-600">Berbagai lomba teknologi untuk meningkatkan skill mahasiswa.</p>
          </div>
          <div class="bg-white p-6 rounded-xl shadow">
            <h4 class="font-bold text-lg mb-2">Pengabdian</h4>
            <p class="text-gray-600">Kegiatan sosial dan pengabdian masyarakat.</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="container mx-auto py-16 px-4">
      <h3 class="text-2xl font-bold mb-6">Kontak</h3>
      <p class="text-gray-700">Email: himatif@unib.ac.id</p>
    </section>

    <!-- Footer -->
    <footer class="bg-gray-800 text-white text-center py-6 mt-auto">
      <p>&copy; 2025 HIMATIF Universitas Bengkulu</p>
    </footer>
  </div>
</template>
