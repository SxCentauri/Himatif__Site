<script setup>
import { Link } from '@inertiajs/vue3'
import { onMounted, onUnmounted, ref } from 'vue'

// ✅ State untuk mobile menu
const isMobileMenuOpen = ref(false)

// ✅ Toggle mobile menu
const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value
}

// ✅ Handle scroll effect (ubah navbar)
const handleScroll = () => {
  const navbar = document.querySelector('.navbar')
  if (navbar) {
    if (window.scrollY > 50) {
      navbar.classList.add('scrolled')
    } else {
      navbar.classList.remove('scrolled')
    }
  }
}

// ✅ Close mobile menu ketika klik link
const closeMobileMenu = () => {
  isMobileMenuOpen.value = false
}

onMounted(() => {
  // ---- NAVBAR ----
  window.addEventListener('scroll', handleScroll)
  document.documentElement.style.scrollBehavior = 'smooth'
  document.addEventListener('click', (e) => {
    const navbar = document.querySelector('.navbar')
    if (navbar && !navbar.contains(e.target)) {
      isMobileMenuOpen.value = false
    }
  })

  // ---- Active NavLink ----
  const links = document.querySelectorAll('.nav-link')
  const currentPath = window.location.pathname
  links.forEach(link => {
    if (link.getAttribute('href') === currentPath) {
      link.classList.add('active')
    }
  })

  // ---- AOS ----
  import("aos").then((AOS) => {
    AOS.init({
      duration: 1000,
      once: true,
      easing: "ease-out-quart",
      offset: 100,
    });
  });

  // ---- Swiper ----
  import("swiper/bundle").then(({ default: Swiper }) => {
    new Swiper(".mySwiper", {
      slidesPerView: 1,
      spaceBetween: 20,
      loop: true,
      autoplay: {
        delay: 3500,
        disableOnInteraction: false,
      },
      pagination: {
        el: ".swiper-pagination",
        clickable: true,
      },
      breakpoints: {
        768: { slidesPerView: 2 },
        1024: { slidesPerView: 3 },
      },
    });
  });

  // ---- FAQ Accordion ----
  const faqHeaders = document.querySelectorAll(".faq-header");
  faqHeaders.forEach((header) => {
    header.addEventListener("click", function () {
      const faqItem = this.parentElement;
      const content = this.nextElementSibling;
      const chevron = this.querySelector(".faq-chevron");

      document.querySelectorAll(".faq-item").forEach((item) => {
        if (item !== faqItem) {
          item.classList.remove("active");
          item.querySelector(".faq-content").classList.remove("max-h-96", "opacity-100");
          item.querySelector(".faq-content").classList.add("max-h-0", "opacity-0");
          item.querySelector(".faq-chevron").classList.remove("rotate-180");
        }
      });

      const isActive = faqItem.classList.contains("active");
      if (isActive) {
        faqItem.classList.remove("active");
        content.classList.remove("max-h-96", "opacity-100");
        content.classList.add("max-h-0", "opacity-0");
        chevron.classList.remove("rotate-180");
      } else {
        faqItem.classList.add("active");
        content.classList.remove("max-h-0", "opacity-0");
        content.classList.add("max-h-96", "opacity-100");
        chevron.classList.add("rotate-180");
      }
    });
  });

  // ---- Newsletter Validation ----
  const newsletterForm = document.querySelector(".newsletter-btn");
  if (newsletterForm) {
    newsletterForm.addEventListener("click", function (e) {
      e.preventDefault();
      const emailInput = document.querySelector('input[type="email"]');
      if (emailInput.value === "" || !emailInput.value.includes("@")) {
        emailInput.focus();
        emailInput.classList.add("ring-2", "ring-red-500");
      } else {
        emailInput.classList.remove("ring-2", "ring-red-500");
        alert("Terima kasih telah berlangganan newsletter kami!");
        emailInput.value = "";
      }
    });
  }

  // ---- Background Particle Animation ----
  function createParticle() {
    const particle = document.createElement("div");
    particle.className = "particle";
    particle.style.left = Math.random() * 100 + "%";
    particle.style.width = particle.style.height = Math.random() * 4 + 2 + "px";
    particle.style.animationDelay = Math.random() * 8 + "s";
    const bg = document.querySelector(".bg-animated");
    if (bg) bg.appendChild(particle);
    setTimeout(() => { particle.remove(); }, 8000);
  }
  setInterval(createParticle, 2000);

  // ---- Button Animation ----
  document.querySelectorAll("button").forEach((button) => {
    button.addEventListener("click", function () {
      this.style.transform = "scale(0.95)";
      setTimeout(() => { this.style.transform = ""; }, 150);
    });
  });
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
  <div class="bg-gray-900 text-gray-100">
    <!-- Navbar -->
    <header class="navbar fixed w-full z-50 bg-gray-900/80 backdrop-blur-md shadow-md">
      <nav class="nav-container container mx-auto flex justify-between items-center py-4 px-6">
        <!-- Logo + Text -->
        <Link href="/" class="logo flex items-center space-x-3">
        <img src="./img/himatif.png" alt="HIMATIF Logo" class="logo-img h-10 w-10 object-contain" />
        <span class="logo-text text-2xl font-bold text-blue-400">HIMATIF UNIB</span>
        </Link>

        <!-- Menu -->
        <ul class="nav-links hidden md:flex space-x-8 text-gray-200">
          <li>
            <Link href="/" class="nav-link" :class="{ 'active': route().current('home') }">Home</Link>
          </li>
          <li>
            <Link href="/about" class="nav-link" :class="{ 'active': route().current('about') }">About Us</Link>
          </li>
          <li>
            <Link href="/profiles" class="nav-link" :class="{ 'active': route().current('profile') }">Profile</Link>
          </li>
          <li>
            <Link href="/proker" class="nav-link" :class="{ 'active': route().current('proker') }">Proker</Link>
          </li>
          <li>
            <Link href="/academic" class="nav-link" :class="{ 'active': route().current('academic') }">Academic</Link>
          </li>
          <li>
            <Link href="/aspiration" class="nav-link" :class="{ 'active': route().current('aspiration') }">Aspiration
            </Link>
          </li>
        </ul>

        <!-- Mobile Menu Button -->
        <button class="mobile-menu-btn">
          <i class="fas fa-bars"></i>
        </button>
      </nav>
    </header>

    <!-- Hero Section -->
    <section id="home" class="min-h-screen flex items-center bg-animated pt-24 px-6 md:px-20 relative overflow-hidden">
      <!-- Animated Background Particles -->
      <div class="absolute inset-0 pointer-events-none">
        <div class="particle" style="left: 10%; width: 4px; height: 4px; animation-delay: 0s;"></div>
        <div class="particle" style="left: 20%; width: 6px; height: 6px; animation-delay: 2s;"></div>
        <div class="particle" style="left: 30%; width: 3px; height: 3px; animation-delay: 4s;"></div>
        <div class="particle" style="left: 40%; width: 5px; height: 5px; animation-delay: 6s;"></div>
        <div class="particle" style="left: 50%; width: 4px; height: 4px; animation-delay: 8s;"></div>
        <div class="particle" style="left: 60%; width: 6px; height: 6px; animation-delay: 1s;"></div>
        <div class="particle" style="left: 70%; width: 3px; height: 3px; animation-delay: 3s;"></div>
        <div class="particle" style="left: 80%; width: 5px; height: 5px; animation-delay: 5s;"></div>
        <div class="particle" style="left: 90%; width: 4px; height: 4px; animation-delay: 7s;"></div>
      </div>

      <!-- Glass Effect Overlay -->
      <div class="absolute inset-0 bg-gradient-to-r from-black/20 via-transparent to-black/10"></div>

      <div class="grid grid-cols-1 lg:grid-cols-2 gap-16 items-center w-full relative z-10">

        <!-- Left: Enhanced Text Content -->
        <div class="text-center lg:text-left space-y-8" data-aos="fade-right" data-aos-duration="1000">
          <!-- Badge -->
          <div class="inline-block glass-effect px-6 py-3 rounded-full text-blue-300 text-sm font-medium mb-6">
            🚀 Teknologi • Inovasi • Komunitas
          </div>

          <!-- Main Heading -->
          <h1 class="text-5xl md:text-7xl lg:text-8xl font-black text-white leading-tight text-shadow">
            Welcome to
            <span class="block gradient-text mt-2">HIMATIF UNIB</span>
          </h1>

          <!-- Subtitle -->
          <div class="space-y-4">
            <p class="text-xl md:text-2xl text-gray-200 max-w-2xl leading-relaxed">
              Himpunan Mahasiswa Teknik Informatika Universitas Bengkulu
            </p>
            <p class="text-lg md:text-xl text-blue-200 max-w-xl opacity-90">
              Wadah kreativitas, inovasi, dan kebersamaan untuk masa depan teknologi yang lebih cerah
            </p>
          </div>



          <!-- Stats -->
          <div class="grid grid-cols-3 gap-8 pt-8" data-aos="fade-up" data-aos-delay="700">
            <div class="text-center">
              <div class="text-3xl md:text-4xl font-bold gradient-text">500+</div>
              <div class="text-gray-300 text-sm mt-1">Anggota Aktif</div>
            </div>
            <div class="text-center">
              <div class="text-3xl md:text-4xl font-bold gradient-text">50+</div>
              <div class="text-gray-300 text-sm mt-1">Event Tahunan</div>
            </div>
            <div class="text-center">
              <div class="text-3xl md:text-4xl font-bold gradient-text">15+</div>
              <div class="text-gray-300 text-sm mt-1">Tahun Berdiri</div>
            </div>
          </div>
        </div>

        <!-- Right: Enhanced Image Section -->
        <div class="flex justify-center lg:justify-end" data-aos="fade-left" data-aos-delay="300"
          data-aos-duration="1000">
          <div class="relative">
            <!-- Background Glow Effect -->
            <div
              class="absolute -inset-4 bg-gradient-to-r from-blue-600 via-purple-600 to-blue-800 rounded-3xl blur-3xl opacity-30 pulse-glow">
            </div>

            <!-- Main Image Container -->
            <div class="relative glass-effect p-6 rounded-3xl floating-animation">
              <img src="./img/himatif.png" alt="HIMATIF UNIB Logo"
                class="w-full max-w-lg h-auto rounded-2xl shadow-2xl transform transition-transform duration-300 hover:scale-105" />

              <!-- Decorative Elements -->
              <div
                class="absolute -top-4 -right-4 w-24 h-24 bg-gradient-to-br from-blue-400 to-purple-600 rounded-full opacity-20 blur-xl">
              </div>
              <div
                class="absolute -bottom-6 -left-6 w-32 h-32 bg-gradient-to-br from-purple-400 to-blue-600 rounded-full opacity-15 blur-2xl">
              </div>
            </div>

            <!-- Floating Tech Icons -->
            <div class="absolute top-10 -left-8 glass-effect p-3 rounded-xl floating-animation"
              style="animation-delay: -2s;">
              <span class="text-2xl">💻</span>
            </div>
            <div class="absolute bottom-20 -right-8 glass-effect p-3 rounded-xl floating-animation"
              style="animation-delay: -4s;">
              <span class="text-2xl">🚀</span>
            </div>
            <div class="absolute top-1/3 -right-12 glass-effect p-3 rounded-xl floating-animation"
              style="animation-delay: -1s;">
              <span class="text-2xl">⚡</span>
            </div>
          </div>
        </div>

      </div>

      <!-- Bottom Gradient Fade -->
      <div class="absolute bottom-0 left-0 right-0 h-32 bg-gradient-to-t from-gray-900 to-transparent"></div>
    </section>

    <section id="about" class="relative py-28 bg-gradient-to-b from-gray-900 to-gray-950 overflow-hidden">
      <div class="container mx-auto px-6 md:px-12 text-center relative z-10">
        <!-- Badge -->
        <span
          class="enhanced-badge px-6 py-3 rounded-full text-sm text-blue-400 border border-blue-500/30 bg-blue-500/10"
          data-aos="fade-down">
          About HIMATIF
        </span>

        <!-- Title -->
        <h2 class="section-title text-4xl md:text-5xl font-bold text-white mt-6 mb-8" data-aos="fade-up">
          About HIMATIF
        </h2>

        <!-- Desc -->
        <p class="text-gray-300 max-w-3xl mx-auto leading-relaxed mb-16 text-lg" data-aos="fade-up"
          data-aos-delay="200">
          Himpunan Mahasiswa Informatika adalah sebuah Organisasi Kemahasiswaan khusus Jurusan Teknik Informatika
          yang bergerak dalam bidang Akademik maupun Non-Akademik yang dapat menjadi wadah bagi para Mahasiswa
          Jurusan Teknik Informatika.
        </p>

        <!-- Info Cards -->
        <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-4 gap-8 mb-20">
          <div class="info-card" data-aos="zoom-in" data-aos-delay="100">
            <div class="text-blue-400 text-4xl mb-6">📅</div>
            <h3 class="text-xl font-bold text-white mb-3">Est. 2008</h3>
            <p class="text-gray-400 text-sm">15+ years of excellence in nurturing tech talents</p>
          </div>
          <div class="info-card" data-aos="zoom-in" data-aos-delay="200">
            <div class="text-blue-400 text-4xl mb-6">🏛</div>
            <h3 class="text-xl font-bold text-white mb-3">7 Departments</h3>
            <p class="text-gray-400 text-sm">Specialized divisions for comprehensive development</p>
          </div>
          <div class="info-card" data-aos="zoom-in" data-aos-delay="300">
            <div class="text-blue-400 text-4xl mb-6">👥</div>
            <h3 class="text-xl font-bold text-white mb-3">11 Divisions</h3>
            <p class="text-gray-400 text-sm">Focused teams for targeted skill development</p>
          </div>
          <div class="info-card" data-aos="zoom-in" data-aos-delay="400">
            <div class="text-blue-400 text-4xl mb-6">✨</div>
            <h3 class="text-xl font-bold text-white mb-3">20+ Programs</h3>
            <p class="text-gray-400 text-sm">Diverse range of activities and initiatives</p>
          </div>
        </div>

        <!-- Mission & Vision -->
        <div class="grid grid-cols-1 md:grid-cols-2 gap-10">
          <div class="mission-vision-card" data-aos="fade-right">
            <h3 class="text-2xl font-bold text-blue-400 mb-4">Our Mission</h3>
            <p class="text-gray-300 text-lg">
              Menjadi wadah pengembangan potensi mahasiswa Teknik Informatika yang berkualitas, inovatif, dan berdaya
              saing global melalui kegiatan akademik dan non-akademik yang terstruktur dan berkelanjutan.
            </p>
          </div>
          <div class="mission-vision-card" data-aos="fade-left">
            <h3 class="text-2xl font-bold text-blue-400 mb-4">Our Vision</h3>
            <p class="text-gray-300 text-lg">
              Membangun generasi teknologi yang unggul, berkarakter, dan berkontribusi positif bagi perkembangan
              teknologi informasi di Indonesia melalui berbagai program dan kegiatan yang bermanfaat.
            </p>
          </div>
        </div>
      </div>
      <div class="floating-orb-1"></div>
      <div class="floating-orb-2"></div>
      <div class="floating-orb-3"></div>
    </section>



    <section id="testimonials" class="py-20 bg-gradient-to-b from-gray-900 to-blue-950 relative overflow-hidden">
      <!-- Floating Background Elements -->
      <div class="absolute inset-0">
        <div class="floating-orb-1"></div>
        <div class="floating-orb-2"></div>
      </div>

      <div class="container mx-auto px-6 md:px-12 text-center relative z-10">
        <!-- Heading -->
        <span class="badge px-6 py-2 rounded-full text-sm bg-blue-800/50 text-blue-300 border border-blue-600/30"
          data-aos="fade-up">
          Testimonials
        </span>
        <h2 class="section-title text-3xl md:text-4xl font-bold text-white mt-4 mb-4" data-aos="fade-up"
          data-aos-delay="100">
          What They Say
        </h2>
        <p class="text-gray-400 max-w-2xl mx-auto mb-12" data-aos="fade-up" data-aos-delay="200">
          Dengarkan pengalaman dan cerita dari para alumni HIMATIF UNIB yang telah sukses dalam karir mereka.
        </p>

        <!-- Swiper -->
        <div class="swiper mySwiper" data-aos="zoom-in" data-aos-delay="300">
          <div class="swiper-wrapper">
            <!-- Testimoni 1 -->
            <div class="swiper-slide ">
              <div
                class="testimonial-card mt-8 bg-gray-800/80 p-8 rounded-2xl shadow-lg h-full flex flex-col justify-between min-h-[480px] max-w-[320px] mx-auto z-0 backdrop-blur-sm border border-gray-700/50">
                <div class="quote-icon mb-4">
                  <svg class="w-8 h-8 text-blue-400 mx-auto" fill="currentColor" viewBox="0 0 24 24">
                    <path
                      d="M14.017 21v-7.391c0-5.704 3.731-9.57 8.983-10.609l.995 2.151c-2.432.917-3.995 3.638-3.995 5.849h4v10h-10zm-14.017 0v-7.391c0-5.704 3.748-9.57 9-10.609l.996 2.151c-2.433.917-3.996 3.638-3.996 5.849h4v10h-10z" />
                  </svg>
                </div>
                <p class="quote-text text-gray-300 italic mb-8 text-lg leading-relaxed">
                  "Bergabung dengan HIMATIF UNIB memberikan saya lebih dari sekadar pengalaman berorganisasi.
                  Di sini saya menemukan keluarga, tempat karakter dibentuk, dan peluang besar untuk berkembang."
                </p>
                <div class="profile-section flex items-center gap-4 mt-auto">
                  <div class="profile-img-container">
                    <img src="./img/profile1.png" alt="Naufal Nazhif A."
                      class="profile-img w-16 h-16 rounded-full border-2 border-blue-400 object-cover" />
                    <div class="absolute inset-0 rounded-full bg-blue-400/20 opacity-0 transition-opacity duration-300">
                    </div>
                  </div>
                  <div class="text-left">
                    <h4 class="profile-name font-semibold text-white text-lg">Naufal Nazhif A.</h4>
                    <p class="profile-position text-sm text-blue-400 mt-1">Wakil Kepala Dinas PMB</p>
                  </div>
                </div>
              </div>
            </div>

            <!-- Testimoni 2 -->
            <div class="swiper-slide">
              <div
                class="testimonial-card mt-8 bg-gray-800/80 p-8 rounded-2xl shadow-lg h-full flex flex-col justify-between min-h-[480px] max-w-[320px] mx-auto z-0 backdrop-blur-sm border border-gray-700/50">
                <div class="quote-icon mb-4">
                  <svg class="w-8 h-8 text-blue-400 mx-auto" fill="currentColor" viewBox="0 0 24 24">
                    <path
                      d="M14.017 21v-7.391c0-5.704 3.731-9.57 8.983-10.609l.995 2.151c-2.432.917-3.995 3.638-3.995 5.849h4v10h-10zm-14.017 0v-7.391c0-5.704 3.748-9.57 9-10.609l.996 2.151c-2.433.917-3.996 3.638-3.996 5.849h4v10h-10z" />
                  </svg>
                </div>
                <p class="quote-text text-gray-300 italic mb-8 text-lg leading-relaxed">
                  "Menjadi bagian dari HIMATIF UNIB adalah salah satu pengalaman paling berkesan.
                  Saya belajar kepemimpinan, manajemen, dan membangun relasi yang luas."
                </p>
                <div class="profile-section flex items-center gap-4 mt-auto">
                  <div class="profile-img-container relative">
                    <img src="./img/profile1.png" alt="M Dzawil Fadhol A."
                      class="profile-img w-16 h-16 rounded-full border-2 border-blue-400 object-cover" />
                  </div>
                  <div class="text-left">
                    <h4 class="profile-name font-semibold text-white text-lg">M Dzawil Fadhol A.</h4>
                    <p class="profile-position text-sm text-blue-400 mt-1">Ketua Himpunan Mahasiswa Informatika</p>
                  </div>
                </div>
              </div>
            </div>

            <!-- Testimoni 3 -->
            <div class="swiper-slide">
              <div
                class="testimonial-card mt-8 bg-gray-800/80 p-8 rounded-2xl shadow-lg h-full flex flex-col justify-between min-h-[480px] max-w-[320px] mx-auto z-0 backdrop-blur-sm border border-gray-700/50">
                <div class="quote-icon mb-4">
                  <svg class="w-8 h-8 text-blue-400 mx-auto" fill="currentColor" viewBox="0 0 24 24">
                    <path
                      d="M14.017 21v-7.391c0-5.704 3.731-9.57 8.983-10.609l.995 2.151c-2.432.917-3.995 3.638-3.995 5.849h4v10h-10zm-14.017 0v-7.391c0-5.704 3.748-9.57 9-10.609l.996 2.151c-2.433.917-3.996 3.638-3.996 5.849h4v10h-10z" />
                  </svg>
                </div>
                <p class="quote-text text-gray-300 italic mb-8 text-lg leading-relaxed">
                  "Merupakan keputusan tepat bergabung dengan HIMATIF. Saya mendapatkan pengalaman baru,
                  relasi luas, dan kesempatan untuk mengasah keterampilan."
                </p>
                <div class="profile-section flex items-center gap-4 mt-auto">
                  <div class="profile-img-container relative">
                    <img src="./img/profile1.png" alt="Vellanindhita"
                      class="profile-img w-16 h-16 rounded-full border-2 border-blue-400 object-cover" />
                  </div>
                  <div class="text-left">
                    <h4 class="profile-name font-semibold text-white text-lg">Vellanindhita</h4>
                    <p class="profile-position text-sm text-blue-400 mt-1">Sekretaris Umum 2</p>
                  </div>
                </div>
              </div>
            </div>

            <!-- Testimoni 4 -->
            <div class="swiper-slide">
              <div
                class="testimonial-card mt-8 bg-gray-800/80 p-8 rounded-2xl shadow-lg h-full flex flex-col justify-between min-h-[480px] max-w-[320px] mx-auto z-0 backdrop-blur-sm border border-gray-700/50">
                <div class="quote-icon mb-4">
                  <svg class="w-8 h-8 text-blue-400 mx-auto" fill="currentColor" viewBox="0 0 24 24">
                    <path
                      d="M14.017 21v-7.391c0-5.704 3.731-9.57 8.983-10.609l.995 2.151c-2.432.917-3.995 3.638-3.995 5.849h4v10h-10zm-14.017 0v-7.391c0-5.704 3.748-9.57 9-10.609l.996 2.151c-2.433.917-3.996 3.638-3.996 5.849h4v10h-10z" />
                  </svg>
                </div>
                <p class="quote-text text-gray-300 italic mb-8 text-lg leading-relaxed">
                  "HIMATIF telah memberikan saya platform untuk mengembangkan diri dan berkontribusi pada komunitas.
                  Pengalaman yang tak terlupakan dengan teman-teman hebat."
                </p>
                <div class="profile-section flex items-center gap-4 mt-auto">
                  <div class="profile-img-container relative">
                    <img src="./img/profile1.png" alt="Alumni"
                      class="profile-img w-16 h-16 rounded-full border-2 border-blue-400 object-cover" />
                  </div>
                  <div class="text-left">
                    <h4 class="profile-name font-semibold text-white text-lg">Rizki Pratama</h4>
                    <p class="profile-position text-sm text-blue-400 mt-1">Software Engineer</p>
                  </div>
                </div>
              </div>
            </div>

            <!-- Testimoni 5 -->
            <div class="swiper-slide">
              <div
                class="testimonial-card mt-8 bg-gray-800/80 p-8 rounded-2xl shadow-lg h-full flex flex-col justify-between min-h-[480px] max-w-[320px] mx-auto z-0 backdrop-blur-sm border border-gray-700/50">
                <div class="quote-icon mb-4">
                  <svg class="w-8 h-8 text-blue-400 mx-auto" fill="currentColor" viewBox="0 0 24 24">
                    <path
                      d="M14.017 21v-7.391c0-5.704 3.731-9.57 8.983-10.609l.995 2.151c-2.432.917-3.995 3.638-3.995 5.849h4v10h-10zm-14.017 0v-7.391c0-5.704 3.748-9.57 9-10.609l.996 2.151c-2.433.917-3.996 3.638-3.996 5.849h4v10h-10z" />
                  </svg>
                </div>
                <p class="quote-text text-gray-300 italic mb-8 text-lg leading-relaxed">
                  "Organisasi ini mengajarkan saya tentang teamwork, leadership, dan problem solving.
                  Skills yang sangat berharga untuk karir di bidang teknologi."
                </p>
                <div class="profile-section flex items-center gap-4 mt-auto">
                  <div class="profile-img-container relative">
                    <img src="./img/profile1.png" alt="Alumni"
                      class="profile-img w-16 h-16 rounded-full border-2 border-blue-400 object-cover" />
                  </div>
                  <div class="text-left">
                    <h4 class="profile-name font-semibold text-white text-lg">Sari Indah</h4>
                    <p class="profile-position text-sm text-blue-400 mt-1">Data Scientist</p>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Pagination -->
          <div class="swiper-pagination mt-8"></div>
        </div>
      </div>
    </section>

    <section id="faq" class="relative py-28 bg-gradient-to-b from-gray-900 to-gray-950 overflow-hidden">
      <!-- Floating Background Elements -->
      <div class="absolute inset-0">
        <div class="floating-orb-1"></div>
        <div class="floating-orb-2"></div>
      </div>

      <div class="container mx-auto px-6 md:px-12 relative z-10">
        <!-- Badge -->
        <span
          class="enhanced-badge px-6 py-3 rounded-full text-sm text-blue-400 border border-blue-500/30 bg-blue-500/10 block w-fit mx-auto"
          data-aos="fade-down">
          FAQ
        </span>

        <!-- Title -->
        <h2 class="section-title text-4xl md:text-5xl font-bold text-white mt-6 mb-8 text-center" data-aos="fade-up">
          Frequently Asked Questions
        </h2>

        <!-- FAQ Container -->
        <div class="faq-container max-w-4xl mx-auto rounded-2xl p-8 shadow-2xl" data-aos="fade-up" data-aos-delay="200">

          <!-- FAQ Items -->
          <div class="space-y-4">

            <!-- FAQ Item 1 -->
            <div class="faq-item rounded-xl transition-all duration-300 ease-out" data-aos="fade-up"
              data-aos-delay="300">
              <button
                class="faq-header w-full flex items-center justify-between p-6 text-left rounded-xl transition-all duration-300">
                <div class="flex items-center space-x-4">
                  <div class="faq-icon w-8 h-8 rounded-full bg-blue-500/20 flex items-center justify-center">
                    <svg class="w-4 h-4 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                        d="M8.228 9c.549-1.165 2.03-2 3.772-2 2.21 0 4 1.343 4 3 0 1.4-1.278 2.575-3.006 2.907-.542.104-.994.54-.994 1.093m0 3h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                    </svg>
                  </div>
                  <h3 class="font-semibold text-lg text-white">Apa itu HIMATIF?</h3>
                </div>
                <div class="faq-chevron transition-transform duration-300">
                  <svg class="w-5 h-5 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
                  </svg>
                </div>
              </button>
              <div class="faq-content overflow-hidden transition-all duration-500 ease-out max-h-0 opacity-0">
                <div class="px-6 pb-6">
                  <div class="pl-12">
                    <p class="text-gray-300 leading-relaxed">
                      Himpunan Mahasiswa Teknik Informatika (HIMATIF) adalah organisasi kemahasiswaan tingkat jurusan
                      yang menaungi seluruh mahasiswa Program Studi Teknik Informatika. HIMATIF berfungsi sebagai wadah
                      untuk mengembangkan potensi akademik dan non-akademik mahasiswa serta menjembatani komunikasi
                      antara mahasiswa, dosen, dan pihak eksternal.
                    </p>
                  </div>
                </div>
              </div>
            </div>

            <!-- FAQ Item 2 -->
            <div class="faq-item rounded-xl transition-all duration-300 ease-out" data-aos="fade-up"
              data-aos-delay="350">
              <button
                class="faq-header w-full flex items-center justify-between p-6 text-left rounded-xl transition-all duration-300">
                <div class="flex items-center space-x-4">
                  <div class="faq-icon w-8 h-8 rounded-full bg-blue-500/20 flex items-center justify-center">
                    <svg class="w-4 h-4 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                        d="M19 11H5m14-5v12a2 2 0 01-2 2H7a2 2 0 01-2-2V6a2 2 0 012-2h10a2 2 0 012 2z" />
                    </svg>
                  </div>
                  <h3 class="font-semibold text-lg text-white">Apa saja Program HIMATIF?</h3>
                </div>
                <div class="faq-chevron transition-transform duration-300">
                  <svg class="w-5 h-5 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
                  </svg>
                </div>
              </button>
              <div class="faq-content overflow-hidden transition-all duration-500 ease-out max-h-0 opacity-0">
                <div class="px-6 pb-6">
                  <div class="pl-12">
                    <p class="text-gray-300 leading-relaxed mb-3">
                      HIMATIF menyelenggarakan berbagai program yang mendukung pengembangan mahasiswa:
                    </p>
                    <ul class="text-gray-300 space-y-2 ml-4">
                      <li>• Workshop dan seminar teknologi terkini</li>
                      <li>• Kompetisi programming dan hackathon</li>
                      <li>• Program mentoring untuk mahasiswa baru</li>
                      <li>• Kegiatan pengabdian masyarakat berbasis teknologi</li>
                      <li>• Event networking dengan industri IT</li>
                    </ul>
                  </div>
                </div>
              </div>
            </div>

            <!-- FAQ Item 3 -->
            <div class="faq-item rounded-xl transition-all duration-300 ease-out" data-aos="fade-up"
              data-aos-delay="400">
              <button
                class="faq-header w-full flex items-center justify-between p-6 text-left rounded-xl transition-all duration-300">
                <div class="flex items-center space-x-4">
                  <div class="faq-icon w-8 h-8 rounded-full bg-blue-500/20 flex items-center justify-center">
                    <svg class="w-4 h-4 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                        d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197m13.5-9a2.5 2.5 0 11-5 0 2.5 2.5 0 015 0z" />
                    </svg>
                  </div>
                  <h3 class="font-semibold text-lg text-white">Bagaimana cara bergabung dengan HIMATIF?</h3>
                </div>
                <div class="faq-chevron transition-transform duration-300">
                  <svg class="w-5 h-5 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
                  </svg>
                </div>
              </button>
              <div class="faq-content overflow-hidden transition-all duration-500 ease-out max-h-0 opacity-0">
                <div class="px-6 pb-6">
                  <div class="pl-12">
                    <p class="text-gray-300 leading-relaxed">
                      Setiap mahasiswa aktif Program Studi Teknik Informatika secara otomatis menjadi anggota HIMATIF.
                      Untuk terlibat aktif dalam kegiatan organisasi, Anda dapat mengikuti rekrutmen pengurus yang
                      biasanya diadakan setiap tahun atau bergabung dalam berbagai kepanitiaan event yang
                      diselenggarakan HIMATIF.
                    </p>
                  </div>
                </div>
              </div>
            </div>

            <!-- FAQ Item 4 -->
            <div class="faq-item rounded-xl transition-all duration-300 ease-out" data-aos="fade-up"
              data-aos-delay="450">
              <button
                class="faq-header w-full flex items-center justify-between p-6 text-left rounded-xl transition-all duration-300">
                <div class="flex items-center space-x-4">
                  <div class="faq-icon w-8 h-8 rounded-full bg-blue-500/20 flex items-center justify-center">
                    <svg class="w-4 h-4 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                        d="M9.663 17h4.673M12 3v1m6.364 1.636l-.707.707M21 12h-1M4 12H3m3.343-5.657l-.707-.707m2.828 9.9a5 5 0 117.072 0l-.548.547A3.374 3.374 0 0014 18.469V19a2 2 0 11-4 0v-.531c0-.895-.356-1.754-.988-2.386l-.548-.547z" />
                    </svg>
                  </div>
                  <h3 class="font-semibold text-lg text-white">Apa manfaat bergabung dengan HIMATIF?</h3>
                </div>
                <div class="faq-chevron transition-transform duration-300">
                  <svg class="w-5 h-5 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
                  </svg>
                </div>
              </button>
              <div class="faq-content overflow-hidden transition-all duration-500 ease-out max-h-0 opacity-0">
                <div class="px-6 pb-6">
                  <div class="pl-12">
                    <p class="text-gray-300 leading-relaxed mb-3">
                      Bergabung dengan HIMATIF memberikan berbagai manfaat untuk pengembangan diri:
                    </p>
                    <ul class="text-gray-300 space-y-2 ml-4">
                      <li>• Mengembangkan soft skills dan leadership</li>
                      <li>• Memperluas jaringan pertemanan dan profesional</li>
                      <li>• Mendapatkan pengalaman organisasi yang valuable</li>
                      <li>• Akses ke workshop dan training eksklusif</li>
                      <li>• Kesempatan magang dan kerja sama dengan industri</li>
                      <li>• Platform untuk mengasah kemampuan public speaking</li>
                    </ul>
                  </div>
                </div>
              </div>
            </div>

            <!-- FAQ Item 5 -->
            <div class="faq-item rounded-xl transition-all duration-300 ease-out" data-aos="fade-up"
              data-aos-delay="500">
              <button
                class="faq-header w-full flex items-center justify-between p-6 text-left rounded-xl transition-all duration-300">
                <div class="flex items-center space-x-4">
                  <div class="faq-icon w-8 h-8 rounded-full bg-blue-500/20 flex items-center justify-center">
                    <svg class="w-4 h-4 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                        d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z" />
                    </svg>
                  </div>
                  <h3 class="font-semibold text-lg text-white">Berapa lama masa kepengurusan HIMATIF?</h3>
                </div>
                <div class="faq-chevron transition-transform duration-300">
                  <svg class="w-5 h-5 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
                  </svg>
                </div>
              </button>
              <div class="faq-content overflow-hidden transition-all duration-500 ease-out max-h-0 opacity-0">
                <div class="px-6 pb-6">
                  <div class="pl-12">
                    <p class="text-gray-300 leading-relaxed">
                      Masa kepengurusan HIMATIF berlangsung selama satu tahun akademik. Periode kepengurusan dimulai
                      dari pelantikan pengurus baru hingga pelantikan pengurus periode berikutnya. Selama masa ini,
                      pengurus akan menjalankan program kerja yang telah direncanakan serta mengkoordinasikan berbagai
                      kegiatan untuk kemajuan organisasi dan anggota.
                    </p>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <footer class="bg-gradient-to-b from-gray-900 to-gray-950 pt-16 pb-8 px-4">
      <!-- Newsletter Section -->
      <div class="container mx-auto max-w-6xl mb-16">
        <div class="flex flex-col md:flex-row items-center justify-between bg-gray-800 rounded-2xl p-8 shadow-xl">
          <div class="mb-6 md:mb-0 md:mr-8">
            <h3 class="text-2xl font-bold text-white mb-2">Stay Updated With HIMATIF</h3>
            <p class="text-gray-400">Subscribe to our newsletter for the latest updates, events, and opportunities.</p>
          </div>
          <div class="flex flex-col sm:flex-row w-full md:w-auto">
            <input type="email" placeholder="Enter your email"
              class="newsletter-input rounded-lg px-4 py-3 sm:rounded-r-none w-full sm:w-64 focus:outline-none focus:ring-2 focus:ring-blue-500">
            <button
              class="newsletter-btn text-white font-semibold rounded-lg px-6 py-3 mt-2 sm:mt-0 sm:rounded-l-none">Subscribe</button>
          </div>
        </div>
      </div>

      <!-- Main Footer Content -->
      <div class="container mx-auto max-w-6xl">
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8 mb-12">
          <!-- Brand Column -->
          <div class="lg:col-span-1">
            <div class="mb-6">
              <h2 class="text-2xl font-bold text-white">HIMATIF</h2>
              <p class="text-lg text-gray-400 mt-1">Himpunan Mahasiswa Teknik Informatika</p>
            </div>
            <p class="text-gray-400 mb-6">HIMATIF Universitas Bengkulu – Wadah kreativitas dan inovasi mahasiswa Teknik
              Informatika.</p>
            <div class="flex space-x-4">
              <a href="#" class="social-icon text-gray-400 hover:text-blue-400 text-xl"><i
                  class="fab fa-facebook"></i></a>
              <a href="#" class="social-icon text-gray-400 hover:text-blue-400 text-xl"><i
                  class="fab fa-twitter"></i></a>
              <a href="#" class="social-icon text-gray-400 hover:text-blue-400 text-xl"><i
                  class="fab fa-instagram"></i></a>
              <a href="#" class="social-icon text-gray-400 hover:text-blue-400 text-xl"><i
                  class="fab fa-linkedin"></i></a>
              <a href="#" class="social-icon text-gray-400 hover:text-blue-400 text-xl"><i
                  class="fab fa-youtube"></i></a>
            </div>
          </div>

          <!-- Menu Column -->
          <div>
            <h3 class="text-lg font-semibold text-white mb-6">Menu</h3>
            <ul class="space-y-3">
              <li><a href="#" class="footer-link text-gray-400 hover:text-white flex items-center"><i
                    class="fas fa-chevron-right text-xs mr-2 text-blue-400"></i> Home</a></li>
              <li><a href="#" class="footer-link text-gray-400 hover:text-white flex items-center"><i
                    class="fas fa-chevron-right text-xs mr-2 text-blue-400"></i> About Us</a></li>
              <li><a href="#" class="footer-link text-gray-400 hover:text-white flex items-center"><i
                    class="fas fa-chevron-right text-xs mr-2 text-blue-400"></i> Profile</a></li>
              <li><a href="#" class="footer-link text-gray-400 hover:text-white flex items-center"><i
                    class="fas fa-chevron-right text-xs mr-2 text-blue-400"></i> Proker</a></li>
              <li><a href="#" class="footer-link text-gray-400 hover:text-white flex items-center"><i
                    class="fas fa-chevron-right text-xs mr-2 text-blue-400"></i> Academic</a></li>
              <li><a href="#" class="footer-link text-gray-400 hover:text-white flex items-center"><i
                    class="fas fa-chevron-right text-xs mr-2 text-blue-400"></i> Aspiration</a></li>
            </ul>
          </div>

          <!-- Informasi Column -->
          <div>
            <h3 class="text-lg font-semibold text-white mb-6">Informasi</h3>
            <ul class="space-y-3">
              <li><a href="#" class="footer-link text-gray-400 hover:text-white flex items-center"><i
                    class="fas fa-chevron-right text-xs mr-2 text-blue-400"></i> Testimonials</a></li>
              <li><a href="#" class="footer-link text-gray-400 hover:text-white flex items-center"><i
                    class="fas fa-chevron-right text-xs mr-2 text-blue-400"></i> FAQ</a></li>
            </ul>
          </div>

          <!-- Contact Column -->
          <div>
            <h3 class="text-lg font-semibold text-white mb-6">About</h3>
            <div class="space-y-4">
              <div class="flex items-start">
                <div class="mt-1 text-blue-400 mr-3"><i class="fas fa-map-marker-alt"></i></div>
                <p class="text-gray-400">Jl. WR. Supratman, Kandang Limun, Kota Bengkulu</p>
              </div>
              <div class="flex items-center">
                <div class="text-blue-400 mr-3"><i class="fas fa-envelope"></i></div>
                <p class="text-gray-400">himatif@unib.ac.id</p>
              </div>
              <div class="flex items-center">
                <div class="text-blue-400 mr-3"><i class="fas fa-phone"></i></div>
                <p class="text-gray-400">+62 895-2961-5638</p>
              </div>
            </div>
          </div>
        </div>

        <!-- Divider -->
        <div class="footer-divider"></div>

        <!-- Copyright -->
        <div class="flex flex-col md:flex-row justify-between items-center pt-6">
          <p class="text-gray-500 text-sm mb-4 md:mb-0">© 2025 HIMATIF. Made with <span class="text-red-500">❤</span> by
            HIMATIF Kominfo Team</p>
          <div class="flex space-x-6 text-sm text-gray-500">
            <a href="#" class="hover:text-blue-400 transition-colors">Privacy Policy</a>
            <a href="#" class="hover:text-blue-400 transition-colors">Terms of Service</a>
            <a href="#" class="hover:text-blue-400 transition-colors">Sitemap</a>
          </div>
        </div>
      </div>
    </footer>

  </div>
</template>

<style>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 1000;
  backdrop-filter: blur(10px);
  padding: 1rem 0;
  transition: all 0.3s ease;
}

.navbar.scrolled {
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
  padding: 0.8rem 0;
}

.nav-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 1.5rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  text-decoration: none;
}

.logo-img {
  height: 40px;
  width: 40px;
  object-fit: contain;
}

.logo-text {
  font-size: 1.5rem;
  font-weight: 800;
  color: #60a5fa;
}

.nav-links {
  display: flex;
  gap: 2rem;
  list-style: none;
}

.nav-link {
  color: #e5e7eb;
  text-decoration: none;
  font-weight: 500;
  transition: color 0.3s ease;
  position: relative;
}

.nav-link:hover {
  color: #60a5fa;
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: -5px;
  left: 0;
  width: 0;
  height: 2px;
  background: #60a5fa;
  transition: width 0.3s ease;
}

.nav-link:hover::after {
  width: 100%;
}

.nav-link.active::after {
  content: '';
  position: absolute;
  bottom: -5px;
  left: 0;
  width: 100%;
  /* full garis bawah */
  height: 2px;
  background: #60a5fa;
}

.nav-link.active {
  color: #60a5fa;
  /* opsional biar teks ikut biru */
}

.mobile-menu-btn {
  display: none;
  background: none;
  border: none;
  color: #e5e7eb;
  font-size: 1.5rem;
  cursor: pointer;
}

.testimonial-card {
  transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  backdrop-filter: blur(10px);
  position: relative;
  overflow: hidden;
  max-width: 400px;
}

.testimonial-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(59, 130, 246, 0.1), transparent);
  transition: left 0.6s;
}

.testimonial-card:hover::before {
  left: 100%;
}

.testimonial-card:hover {
  transform: scale(1.05) translateY(-8px);
  box-shadow:
    0 25px 50px -12px rgba(59, 130, 246, 0.25),
    0 0 0 1px rgba(59, 130, 246, 0.2);
  background: linear-gradient(135deg,
      rgba(31, 41, 55, 0.95) 0%,
      rgba(30, 58, 138, 0.1) 100%);
}

.testimonial-card:hover .quote-text {
  color: #f3f4f6;
  transform: translateY(-2px);
}

.testimonial-card:hover .profile-img {
  transform: scale(1.15);
  box-shadow: 0 8px 25px -8px rgba(59, 130, 246, 0.5);
  border-color: #60a5fa;
}

.testimonial-card:hover .profile-name {
  color: #60a5fa;
  text-shadow: 0 0 10px rgba(96, 165, 250, 0.3);
}

.testimonial-card:hover .profile-position {
  color: #93c5fd;
}

.testimonial-card:hover .quote-icon svg {
  color: #60a5fa;
  transform: scale(1.1);
}

/* Smooth Transitions */
.quote-text,
.profile-img,
.profile-name,
.profile-position,
.quote-icon svg {
  transition: all 0.3s ease;
}

/* Enhanced Badge */
.badge,
.enhanced-badge {
  background: linear-gradient(135deg,
      rgba(59, 130, 246, 0.2),
      rgba(29, 78, 216, 0.3));
  backdrop-filter: blur(10px);
  transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  position: relative;
  overflow: hidden;
}

.badge::before,
.enhanced-badge::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(59, 130, 246, 0.3), transparent);
  transition: left 0.6s;
}

.badge:hover,
.enhanced-badge:hover {
  transform: scale(1.1) translateY(-2px);
  background: rgba(59, 130, 246, 0.2);
  border-color: rgba(59, 130, 246, 0.6);
  box-shadow: 0 10px 25px -5px rgba(59, 130, 246, 0.3);
}

.badge:hover::before,
.enhanced-badge:hover::before {
  left: 100%;
}

/* Info Cards */
.info-card {
  background: rgba(31, 41, 55, 0.8);
  padding: 2rem;
  border-radius: 1rem;
  border: 1px solid rgba(75, 85, 99, 0.5);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
  position: relative;
  overflow: hidden;
  transition: all 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  cursor: pointer;
}

.info-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(59, 130, 246, 0.1), transparent);
  transition: left 0.8s;
}

.info-card:hover::before {
  left: 100%;
}

.info-card:hover {
  transform: scale(1.15) translateY(-15px) rotateY(5deg);
  box-shadow:
    0 30px 60px -10px rgba(59, 130, 246, 0.4),
    0 0 0 1px rgba(59, 130, 246, 0.3);
  background: linear-gradient(135deg,
      rgba(31, 41, 55, 0.95) 0%,
      rgba(30, 58, 138, 0.2) 100%);
  border-color: rgba(59, 130, 246, 0.5);
}

/* Mission & Vision Cards */
.mission-vision-card {
  background: rgba(31, 41, 55, 0.8);
  padding: 2rem;
  border-radius: 1rem;
  border: 1px solid rgba(75, 85, 99, 0.5);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
  position: relative;
  overflow: hidden;
  transition: all 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  cursor: pointer;
}

.mission-vision-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(59, 130, 246, 0.1), transparent);
  transition: left 1s;
}

.mission-vision-card:hover::before {
  left: 100%;
}

.mission-vision-card:hover {
  transform: scale(1.08) translateY(-12px) perspective(1000px) rotateX(5deg);
  box-shadow:
    0 35px 70px -15px rgba(59, 130, 246, 0.4),
    0 0 0 1px rgba(59, 130, 246, 0.3);
  background: linear-gradient(135deg,
      rgba(31, 41, 55, 0.9) 0%,
      rgba(30, 58, 138, 0.15) 100%);
  border-color: rgba(59, 130, 246, 0.5);
}

.mission-vision-card:hover h3 {
  color: #60a5fa;
  text-shadow: 0 0 15px rgba(96, 165, 250, 0.6);
  transform: translateY(-3px);
}

.mission-vision-card:hover p {
  color: #f3f4f6;
  transform: translateY(-2px);
}

/* Section Title */
.section-title {
  background: linear-gradient(135deg, #ffffff, #93c5fd, #60a5fa);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  transition: all 0.3s ease;
}

/* Floating Orbs */
.floating-orb-1,
.floating-orb-2,
.floating-orb-3 {
  position: absolute;
  border-radius: 50%;
  opacity: 0.15;
  pointer-events: none;
  filter: blur(40px);
  animation-timing-function: ease-in-out;
  animation-iteration-count: infinite;
}

.floating-orb-1 {
  width: 400px;
  height: 400px;
  background: linear-gradient(135deg, #3b82f6, #1d4ed8);
  top: 5%;
  left: -10%;
  animation: float1 12s ease-in-out infinite, enhanced-pulse 4s ease-in-out infinite;
}

.floating-orb-2 {
  width: 300px;
  height: 300px;
  background: linear-gradient(135deg, #6366f1, #3730a3);
  bottom: -10%;
  right: -5%;
  animation: float2 15s ease-in-out infinite reverse, enhanced-pulse 4s ease-in-out infinite;
}

.floating-orb-3 {
  width: 250px;
  height: 250px;
  background: linear-gradient(135deg, #8b5cf6, #5b21b6);
  top: 40%;
  right: 10%;
  animation: float3 18s ease-in-out infinite, enhanced-pulse 4s ease-in-out infinite;
}

/* Animations */
@keyframes float1 {

  0%,
  100% {
    transform: translateY(0px) translateX(0px) rotate(0deg) scale(1);
  }

  25% {
    transform: translateY(-30px) translateX(20px) rotate(90deg) scale(1.1);
  }

  50% {
    transform: translateY(-15px) translateX(-15px) rotate(180deg) scale(0.9);
  }

  75% {
    transform: translateY(-40px) translateX(10px) rotate(270deg) scale(1.05);
  }
}

@keyframes float2 {

  0%,
  100% {
    transform: translateY(0px) translateX(0px) rotate(0deg) scale(1);
  }

  33% {
    transform: translateY(-25px) translateX(-25px) rotate(120deg) scale(1.08);
  }

  66% {
    transform: translateY(-35px) translateX(15px) rotate(240deg) scale(0.95);
  }
}

@keyframes float3 {

  0%,
  100% {
    transform: translateY(0px) translateX(0px) rotate(0deg) scale(1);
  }

  20% {
    transform: translateY(-20px) translateX(-10px) rotate(72deg) scale(1.12);
  }

  40% {
    transform: translateY(-35px) translateX(20px) rotate(144deg) scale(0.88);
  }

  60% {
    transform: translateY(-25px) translateX(-20px) rotate(216deg) scale(1.06);
  }

  80% {
    transform: translateY(-40px) translateX(10px) rotate(288deg) scale(0.92);
  }
}

@keyframes enhanced-pulse {

  0%,
  100% {
    opacity: 0.15;
    transform: scale(1);
  }

  50% {
    opacity: 0.25;
    transform: scale(1.05);
  }
}

/* Swiper Pagination */
.swiper-pagination-bullet {
  background: rgba(59, 130, 246, 0.4);
  opacity: 1;
  transition: all 0.3s ease;
}

.swiper-pagination-bullet-active {
  background: #3b82f6;
  transform: scale(1.3);
  box-shadow: 0 0 10px rgba(59, 130, 246, 0.5);
}

.swiper-pagination-bullet:hover {
  background: #60a5fa;
  transform: scale(1.1);
}

/* Global Smooth Scroll */
html {
  scroll-behavior: smooth;
}

/* Swiper Container Spacing */
.mySwiper {
  padding-bottom: 3rem;
}

/* FAQ Styles */
.faq-container {
  background: rgba(31, 41, 55, 0.8);
  border: 1px solid rgba(75, 85, 99, 0.5);
  backdrop-filter: blur(10px);
}

.faq-item {
  background: rgba(17, 24, 39, 0.6);
  border: 1px solid rgba(55, 65, 81, 0.5);
  overflow: hidden;
}

.faq-header {
  background: rgba(17, 24, 39, 0.4);
  transition: all 0.3s ease;
}

.faq-header:hover {
  background: rgba(30, 58, 138, 0.2);
}

.faq-content {
  transition: all 0.5s ease-out;
}

/* Mobile Responsiveness */
@media (max-width: 768px) {
  .testimonial-card {
    min-height: 450px;
    padding: 1.5rem;
  }

  .testimonial-card:hover {
    transform: scale(1.02) translateY(-4px);
  }

  .info-card:hover,
  .mission-vision-card:hover {
    transform: scale(1.05) translateY(-8px);
  }

  .floating-orb-1,
  .floating-orb-2,
  .floating-orb-3 {
    opacity: 0.08;
    filter: blur(30px);
  }

  .info-card,
  .mission-vision-card {
    padding: 1.5rem;
  }
}

.footer-divider {
  border-top: 1px solid rgba(100, 116, 139, 0.3);
  margin: 2rem 0;
}

.social-icon {
  transition: all 0.3s ease;
}

.social-icon:hover {
  transform: translateY(-3px);
  color: #3b82f6;
}

.newsletter-input {
  background: rgba(30, 41, 59, 0.5);
  border: 1px solid rgba(100, 116, 139, 0.3);
  transition: all 0.3s ease;
}

.newsletter-input:focus {
  outline: none;
  border-color: #3b82f6;
  box-shadow: 0 0 0 2px rgba(59, 130, 246, 0.2);
}

.newsletter-btn {
  background: linear-gradient(135deg, #3b82f6, #2563eb);
  transition: all 0.3s ease;
}

.newsletter-btn:hover {
  background: linear-gradient(135deg, #2563eb, #1d4ed8);
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(37, 99, 235, 0.3);
}

.footer-link {
  transition: all 0.2s ease;
}

.footer-link:hover {
  color: #3b82f6;
  transform: translateX(5px);
}

.gradient-text {
  background: linear-gradient(135deg, #60a5fa, #3b82f6, #1d4ed8);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.floating-animation {
  animation: float 6s ease-in-out infinite;
}

@keyframes float {

  0%,
  100% {
    transform: translateY(0px);
  }

  50% {
    transform: translateY(-20px);
  }
}

.pulse-glow {
  animation: pulse-glow 2s infinite;
}

@keyframes pulse-glow {

  0%,
  100% {
    box-shadow: 0 0 20px rgba(96, 165, 250, 0.4);
  }

  50% {
    box-shadow: 0 0 40px rgba(96, 165, 250, 0.8);
  }
}

.bg-animated {
  background: linear-gradient(-45deg, #0f172a, #1e293b, #0c4a6e, #1e3a8a);
  background-size: 400% 400%;
  animation: gradient-shift 15s ease infinite;
}

@keyframes gradient-shift {
  0% {
    background-position: 0% 50%;
  }

  50% {
    background-position: 100% 50%;
  }

  100% {
    background-position: 0% 50%;
  }
}

.glass-effect {
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.2);
}

.text-shadow {
  text-shadow: 0 4px 8px rgba(0, 0, 0, 0.5);
}

.particle {
  position: absolute;
  border-radius: 50%;
  background: rgba(96, 165, 250, 0.6);
  animation: particle-float 8s infinite linear;
  pointer-events: none;
}

@keyframes particle-float {
  0% {
    transform: translateY(100vh) rotate(0deg);
    opacity: 0;
  }

  10% {
    opacity: 1;
  }

  90% {
    opacity: 1;
  }

  100% {
    transform: translateY(-10vh) rotate(360deg);
    opacity: 0;
  }
}
</style>