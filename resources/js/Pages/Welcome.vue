<script setup>
</script>

<template>
    <div class="bg-gray-900 text-gray-100">
      <!-- Navbar -->
      <header class="fixed w-full z-50 bg-gray-900/80 backdrop-blur-md shadow-md">
        <nav class="container mx-auto flex justify-between items-center py-4 px-6">
          <div class="text-2xl font-bold text-blue-400">HIMATIF UNIB</div>
          <ul class="hidden md:flex space-x-8 text-gray-200">
            <li><a href="#home" class="hover:text-blue-400 transition">Home</a></li>
            <li><a href="#about" class="hover:text-blue-400 transition">About</a></li>
            <li><a href="#testimonials" class="hover:text-blue-400 transition">Testimonials</a></li>
            <li><a href="#faq" class="hover:text-blue-400 transition">FAQ</a></li>
          </ul>
        </nav>
      </header>
  
      <!-- Hero Section -->
<section id="home" class="min-h-screen flex items-center bg-gradient-to-b from-gray-900 to-blue-950 pt-24 px-6 md:px-20">
  <div class="grid grid-cols-1 md:grid-cols-2 gap-10 items-center w-full">
    
    <!-- Left: Text -->
    <div class="text-center md:text-left" data-aos="fade-right">
      <h1 class="text-4xl md:text-6xl font-extrabold text-white mb-6">
        Welcome to <span class="text-blue-400">HIMATIF UNIB</span>
      </h1>
      <p class="text-lg md:text-xl text-gray-300 max-w-xl">
        Himpunan Mahasiswa Teknik Informatika Universitas Bengkulu – wadah kreativitas, inovasi, dan kebersamaan.
      </p>
    </div>

    <!-- Right: Image -->
    <div class="flex justify-center md:justify-end" data-aos="fade-left" data-aos-delay="300">
      <img src="./img/himatif.png" 
           alt="Hero" 
           class="w-3/4 md:w-full max-w-md rounded-xl shadow-lg"/>
    </div>

  </div>
</section>
  
      <!-- About Section -->
      <section id="about" class="py-40 bg-gray-900">
  <div class="container mx-auto px-6 md:px-12 text-center">
    <h2 class="text-3xl md:text-4xl font-bold text-white mb-12" data-aos="fade-up">
      About HIMATIF
    </h2>
    <div class="grid md:grid-cols-2 gap-12 items-center">
      
      <!-- Gambar -->
      <div data-aos="fade-right">
        <img src="./img/Hero.png" alt="About HIMATIF" 
             class="w-3/4 md:w-full max-w-xl rounded-xl shadow-lg mx-auto"/>
      </div>

      <!-- Teks -->
      <div data-aos="fade-left" class="text-left">
        <p class="text-gray-300 leading-relaxed text-lg mb-4">
          HIMATIF UNIB adalah organisasi mahasiswa yang berfokus pada pengembangan akademik, peningkatan softskill, serta memperkuat solidaritas antar mahasiswa Teknik Informatika Universitas Bengkulu.
        </p>
        <p class="text-gray-300 leading-relaxed text-lg mb-4">
          Sebagai wadah resmi bagi seluruh mahasiswa, HIMATIF hadir untuk mendukung proses belajar di dalam maupun di luar kelas, memfasilitasi kreativitas melalui berbagai program kerja, serta mendorong inovasi di bidang teknologi dan informasi.
        </p>
        <p class="text-gray-300 leading-relaxed text-lg mb-4">
          Kami berkomitmen untuk menciptakan lingkungan yang inklusif, kolaboratif, dan inspiratif, sehingga setiap anggota dapat mengembangkan potensi terbaiknya. 
        </p>
        <p class="text-gray-300 leading-relaxed text-lg">
          Selain itu, HIMATIF juga menjadi jembatan dalam membangun relasi yang erat antar mahasiswa, alumni, hingga dunia industri, dengan harapan mampu melahirkan generasi informatika yang unggul, berdaya saing, dan siap menghadapi tantangan global.
        </p>
      </div>

    </div>
  </div>
</section>

<section id="testimonials" class="py-20 bg-gradient-to-b from-gray-900 to-blue-950">
  <div class="container mx-auto px-6 md:px-12 text-center">
    
    <!-- Heading -->
    <span class="px-4 py-1 rounded-full text-sm bg-blue-800/50 text-blue-300" data-aos="fade-up">Testimonials</span>
    <h2 class="text-3xl md:text-4xl font-bold text-white mt-4 mb-4" data-aos="fade-up" data-aos-delay="100">
      What They Say
    </h2>
    <p class="text-gray-400 max-w-2xl mx-auto mb-12" data-aos="fade-up" data-aos-delay="200">
      Dengarkan pengalaman dan cerita dari para alumni HIMATIF UNIB yang telah sukses dalam karir mereka.
    </p>

    <!-- Swiper Container -->
    <div class="swiper mySwiper" data-aos="zoom-in" data-aos-delay="300">
      <div class="swiper-wrapper">

        <!-- Testimoni 1 -->
        <div class="swiper-slide">
            <div class="bg-gray-800/80 p-6 rounded-2xl shadow-lg h-full flex flex-col justify-between min-h-[300px]">
            <p class="text-gray-300 italic mb-6">
              “Bergabung dengan HIMATIF UNIB memberikan saya lebih dari sekadar pengalaman berorganisasi. 
              Di sini saya menemukan keluarga, tempat karakter dibentuk, dan peluang besar untuk berkembang.”
            </p>
            <div class="flex items-center gap-4">
              <img src="./img/profile1.png" alt="Mahasiswa" class="w-12 h-12 rounded-full border-2 border-blue-400">
              <div class="text-left">
                <h4 class="font-semibold text-white">Naufal Nazhif A.</h4>
                <p class="text-sm text-blue-400">Wakil Kepala Dinas PMB</p>
              </div>
            </div>
          </div>
        </div>

        <!-- Testimoni 2 -->
        <div class="swiper-slide">
            <div class="bg-gray-800/80 p-6 rounded-2xl shadow-lg h-full flex flex-col justify-between min-h-[300px]">
            <p class="text-gray-300 italic mb-6">
              “Menjadi bagian dari HIMATIF UNIB adalah salah satu pengalaman paling berkesan. 
              Saya belajar kepemimpinan, manajemen, dan membangun relasi yang luas.”
            </p>
            <div class="flex items-center gap-4">
              <img src="./img/profile1.png" alt="Mahasiswa" class="w-12 h-12 rounded-full border-2 border-blue-400">
              <div class="text-left">
                <h4 class="font-semibold text-white">M Dzawil Fadhol A.</h4>
                <p class="text-sm text-blue-400">Ketua Himpunan Mahasiswa Informatika</p>
              </div>
            </div>
          </div>
        </div>

        <!-- Testimoni 3 -->
        <div class="swiper-slide">
            <div class="bg-gray-800/80 p-6 rounded-2xl shadow-lg h-full flex flex-col justify-between min-h-[300px]">
            <p class="text-gray-300 italic mb-6">
              “Merupakan keputusan tepat bergabung dengan HIMATIF. Saya mendapatkan pengalaman baru, 
              relasi luas, dan kesempatan untuk mengasah keterampilan.”
            </p>
            <div class="flex items-center gap-4">
              <img src="./img/profile1.png" alt="Mahasiswa" class="w-12 h-12 rounded-full border-2 border-blue-400">
              <div class="text-left">
                <h4 class="font-semibold text-white">Vellanindhita</h4>
                <p class="text-sm text-blue-400">Sekretaris Umum 2</p>
              </div>
            </div>
          </div>
        </div>

      </div>

      <!-- Pagination -->
      <div class="swiper-pagination mt-6"></div>
    </div>
  </div>
</section>
  
      <!-- FAQ Section -->
      <section id="faq" class="py-20 bg-gray-900">
        <div class="container mx-auto px-6 md:px-12">
          <h2 class="text-3xl md:text-4xl font-bold text-center text-white mb-12" data-aos="fade-up">Frequently Asked Questions</h2>
          <div class="space-y-6 max-w-3xl mx-auto">
            <div class="bg-gray-800 p-6 rounded-xl shadow-md" data-aos="fade-up">
              <h3 class="font-semibold text-blue-400">Apa itu HIMATIF UNIB?</h3>
              <p class="text-gray-300 mt-2">Himpunan Mahasiswa Teknik Informatika Universitas Bengkulu.</p>
            </div>
            <div class="bg-gray-800 p-6 rounded-xl shadow-md" data-aos="fade-up" data-aos-delay="100">
              <h3 class="font-semibold text-blue-400">Bagaimana cara bergabung?</h3>
              <p class="text-gray-300 mt-2">Mahasiswa aktif Teknik Informatika otomatis menjadi anggota HIMATIF.</p>
            </div>
            <div class="bg-gray-800 p-6 rounded-xl shadow-md" data-aos="fade-up" data-aos-delay="200">
              <h3 class="font-semibold text-blue-400">Apa saja kegiatan HIMATIF?</h3>
              <p class="text-gray-300 mt-2">Mulai dari kegiatan akademik, pengabdian masyarakat, hingga event besar bidang IT.</p>
            </div>
          </div>
        </div>
      </section>
  
      <!-- Footer -->
      <footer class="bg-blue-950 py-6 text-center text-gray-400">
        <p>&copy; 2025 HIMATIF UNIB. All rights reserved.</p>
      </footer>
    </div>
  </template>
  
  <script>
  import "swiper/swiper-bundle.css";
  import "aos/dist/aos.css";
  
  export default {
    name: "Home",
    mounted() {
      // Inisialisasi AOS
      import("aos").then((AOS) => {
        AOS.init({
          duration: 1000,
          once: true,
        });
      });
  
      // Inisialisasi Swiper
      import("swiper/bundle").then(({ default: Swiper }) => {
        new Swiper(".mySwiper", {
          slidesPerView: 1,
          spaceBetween: 20,
          loop: true,
          autoplay: {
            delay: 4000,
            disableOnInteraction: false,
          },
          pagination: {
            el: ".swiper-pagination",
            clickable: true,
          },
          breakpoints: {
            768: {
              slidesPerView: 2,
            },
            1024: {
              slidesPerView: 3,
            },
          },
        });
      });
    },
  };
  </script>
  
  <style>
  html {
    scroll-behavior: smooth;
  }
  </style>