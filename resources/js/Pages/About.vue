<script setup>
import { Link } from '@inertiajs/vue3'
import AOS from 'aos'
import 'aos/dist/aos.css'
import { onMounted, nextTick } from 'vue'
import PureCounter from '@srexi/purecounterjs'

onMounted(async () => {
  await nextTick()
  // testt
  AOS.init({
    duration: 1000,
    easing: 'ease-out-cubic',
    once: true,
    offset: 100,
  })

  // ✅ Inisialisasi PureCounter
  try {
    new PureCounter()
  } catch (error) {
    console.log('PureCounter initialization failed:', error)
  }

  // ✅ Smooth scroll behavior
  document.documentElement.style.scrollBehavior = 'smooth'

  // ✅ Navbar scroll effect
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

  window.addEventListener('scroll', handleScroll)

  // ✅ Intersection Observer untuk animasi saat scroll
  const sections = document.querySelectorAll('section')
  const observerOptions = {
    threshold: 0.1,
    rootMargin: '0px 0px -50px 0px',
  }

  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        entry.target.classList.add('visible', 'opacity-100')
        entry.target.classList.remove('opacity-0')
      }
    })
  }, observerOptions)

  sections.forEach((section) => {
    section.classList.add('transition-opacity', 'duration-1000', 'opacity-0')
    observer.observe(section)
  })

  // Cleanup function
  return () => {
    window.removeEventListener('scroll', handleScroll)
    observer.disconnect()
  }
})
</script>

<template>
  <div class="min-h-screen flex flex-col">
    <!-- Navbar -->
    <header class="navbar fixed w-full z-50 bg-gray-900/80 backdrop-blur-md shadow-md">
      <nav class="nav-container container mx-auto flex justify-between items-center py-4 px-6">
        <!-- Logo + Text -->
        <Link href="/" class="logo flex items-center space-x-3">
        <img src="./img/himatif.png" alt="HIMATIF Logo" class="logo-img h-20 w-20 object-contain" />
        <span class="logo-text text-2xl font-bold text-blue-400">HIMATIF UNIB</span>
        </Link>

        <!-- Menu -->
        <ul class="nav-links hidden md:flex space-x-8 text-gray-200">
          <li>
            <Link href="/" class="nav-link hover:text-blue-400 transition">Home</Link>
          </li>
          <li>
            <Link href="/about" class="nav-link hover:text-blue-400 transition">About Us</Link>
          </li>
          <li>
            <Link href="/profile" class="nav-link hover:text-blue-400 transition">Profile</Link>
          </li>
          <li>
            <Link href="/proker" class="nav-link hover:text-blue-400 transition">Proker</Link>
          </li>
          <li>
            <Link href="/academic" class="nav-link hover:text-blue-400 transition">Academic</Link>
          </li>
          <li>
            <Link href="/aspiration" class="nav-link hover:text-blue-400 transition">Aspiration</Link>
          </li>
        </ul>

        <!-- Mobile Menu Button -->
        <button class="mobile-menu-btn">
          <i class="fas fa-bars"></i>
        </button>
      </nav>
    </header>

    <!-- Hero Section -->
    <section id="about" class="hero">
      <div class="hero-content">
        <div class="hero-badge" data-aos="fade-up">
          <span>✨ About HIMATIF UNIB</span>
        </div>

        <h1 class="hero-title" data-aos="fade-up" data-aos-delay="200">
          <span class="gradient-text">Tentang Kami</span>
        </h1>

        <p class="hero-description" data-aos="fade-up" data-aos-delay="400">
          Himpunan Mahasiswa Teknik Informatika Universitas Bengkulu adalah organisasi kemahasiswaan yang berperan
          sebagai wadah pengembangan potensi mahasiswa di bidang teknologi informasi.
        </p>
      </div>

      <div class="scroll-indicator">
        <div class="scroll-circle">
          <div class="scroll-dot"></div>
        </div>
      </div>
    </section>

    <!-- About Section -->
    <section class="section">
      <div class="section-container">
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-16 items-center mb-20">
          <div data-aos="fade-right">
            <h2 class="text-4xl md:text-5xl font-bold mb-8">
              About <span class="gradient-text">HIMATIF</span>
            </h2>
            <p class="text-lg text-gray-300 leading-relaxed mb-6">
              Himpunan Mahasiswa Teknik Informatika (HIMATIF) adalah organisasi kemahasiswaan khusus untuk mahasiswa
              Program Studi Teknik Informatika. Berdiri sejak tahun 2009, HIMATIF berperan sebagai wadah yang mendukung
              pengembangan di bidang akademik dan non-akademik.
            </p>
            <p class="text-lg text-gray-300 leading-relaxed">
              HIMATIF menyediakan berbagai kegiatan yang bermanfaat bagi para mahasiswa serta memiliki beberapa divisi
              yang berfokus pada berbagai aspek untuk meningkatkan kompetensi dan kolaborasi mahasiswa.
            </p>
          </div>

          <div class="flex justify-center" data-aos="fade-left">
            <div class="relative">
              <div
                class="absolute -inset-4 bg-gradient-to-r from-blue-600 via-purple-600 to-blue-800 rounded-3xl blur-3xl opacity-30 pulse-glow">
              </div>
              <div class="glass-effect p-8 rounded-3xl relative floating-animation">
                <img src="./img/himatif.png" alt="HIMATIF Logo" class="w-full max-w-md mx-auto rounded-2xl">
              </div>
            </div>
          </div>
        </div>

        <!-- Statistics -->
        <div class="stats-grid content-section" data-aos="fade-up" data-aos-delay="200">
          <div class="stat-card">
            <div class="stat-number" data-purecounter-start="0" data-purecounter-end="2009"
              data-purecounter-duration="2">2009</div>
            <div class="stat-label">Tahun Berdiri</div>
          </div>

          <div class="stat-card">
            <div class="stat-number" data-purecounter-start="0" data-purecounter-end="6" data-purecounter-duration="1">6
            </div>
            <div class="stat-label">Divisi</div>
          </div>

          <div class="stat-card">
            <div class="stat-number" data-purecounter-start="0" data-purecounter-end="500"
              data-purecounter-duration="2">500+</div>
            <div class="stat-label">Anggota</div>
          </div>

          <div class="stat-card">
            <div class="stat-number" data-purecounter-start="0" data-purecounter-end="25" data-purecounter-duration="2">
              25+</div>
            <div class="stat-label">Kegiatan</div>
          </div>
        </div>

        <!-- Vision & Mission -->
        <div class="section-title content-section" data-aos="fade-up">
          <h2><span class="gradient-text">Visi & Misi</span></h2>
          <p>Komitmen kami dalam mengembangkan generasi teknologi yang unggul dan berkarakter</p>
        </div>

        <div class="vm-grid content-section" data-aos="fade-up" data-aos-delay="200">
          <div class="vm-card vision">
            <div class="vm-header">
              <div class="vm-icon">
                <i class="fas fa-eye"></i>
              </div>
              <h3 class="vm-title">Our Vision</h3>
            </div>

            <p class="vm-content">
              Membangun generasi teknologi yang unggul, berkarakter, dan berkontribusi positif bagi perkembangan
              teknologi informasi di Indonesia melalui berbagai program dan kegiatan yang bermanfaat.
            </p>
          </div>

          <div class="vm-card mission">
            <div class="vm-header">
              <div class="vm-icon">
                <i class="fas fa-bullseye"></i>
              </div>
              <h3 class="vm-title">Our Mission</h3>
            </div>

            <p class="vm-content">
              Menjadi wadah pengembangan potensi mahasiswa Teknik Informatika yang berkualitas, inovatif, dan berdaya
              saing global melalui kegiatan akademik dan non-akademik yang terstruktur dan berkelanjutan.
            </p>
          </div>
        </div>

        <!-- Leadership -->
        <div class="section-title content-section" data-aos="fade-up">
          <h2><span class="gradient-text">HIMATIF Team</span></h2>
          <p>Kepengurusan 2025 - Membangun Generasi Digital yang Unggul</p>
        </div>

        <div class="leadership-content content-section" data-aos="fade-up" data-aos-delay="200">
          <p class="leadership-text">
            Sebagai organisasi mahasiswa, HIMATIF berkomitmen untuk mengembangkan potensi mahasiswa informatika
            melalui berbagai program yang inovatif dan relevan dengan perkembangan teknologi terkini.
          </p>

          <p class="leadership-text">
            Kami percaya bahwa kolaborasi, inovasi, dan pembelajaran berkelanjutan adalah kunci untuk mempersiapkan
            mahasiswa menghadapi tantangan di era digital.
          </p>

          <div class="motto-box">
            <div class="motto gradient-text">"Satukan Visi, Wujudkan Prestasi"</div>
            <div class="motto-label">Motto Kepengurusan 2025</div>
          </div>
        </div>

        <!-- Logo Philosophy -->
        <div class="section-title content-section" data-aos="fade-up">
          <h2><span class="gradient-text">Filosofi Logo</span></h2>
          <p>Makna dan simbolisme di balik identitas visual HIMATIF UNIB</p>
        </div>

        <div class="philosophy-grid content-section" data-aos="fade-up" data-aos-delay="200">
          <div class="philosophy-content">
            <p class="philosophy-text">
              Logo HIMATIF UNIB menggambarkan semangat inovasi, kolaborasi, dan pertumbuhan berkelanjutan dalam
              dunia teknologi informasi. Setiap elemen memiliki makna filosofis yang mendalam.
            </p>

            <div class="meaning-item">
              <div class="meaning-number" style="background: #3B82F6;">6</div>
              <div class="meaning-content">
                <h4>Enam Divisi</h4>
                <p>Melambangkan 6 divisi dalam HIMATIF yang saling bersinergi.</p>
              </div>
            </div>

            <div class="meaning-item">
              <div class="meaning-number" style="background: #8B5CF6;">3</div>
              <div class="meaning-content">
                <h4>Tridharma</h4>
                <p>Melambangkan tridharma perguruan tinggi: pendidikan, penelitian, dan pengabdian.</p>
              </div>
            </div>

            <div class="meaning-item">
              <div class="meaning-number" style="background: #10B981;">5</div>
              <div class="meaning-content">
                <h4>Peran Mahasiswa</h4>
                <p>Melambangkan lima peran mahasiswa sebagai agen perubahan positif.</p>
              </div>
            </div>
          </div>

          <div class="philosophy-visual">
            <div class="logo-visual" style="width: 280px; height: 280px;">
              <div class="logo-glow"></div>
              <div class="logo-main">
                <img src="./img/himatif.png" alt="HIMATIF Logo" style="width: 280px; height: 280px; border-radius: 50%;"
                  onerror="this.style.display='none'; this.parentNode.innerHTML='<span style=\'font-size: 2.5rem; font-weight: 800; color: white;\'>H</span>'" />
              </div>
            </div>
          </div>
        </div>

        <!-- Gallery -->
        <div class="section-title content-section" data-aos="fade-up">
          <h2><span class="gradient-text">Our Gallery</span></h2>
          <p>Dokumentasi kegiatan dan momen berharga HIMATIF Universitas Bengkulu</p>
        </div>

        <div class="gallery-grid content-section" data-aos="fade-up" data-aos-delay="200">
          <div class="gallery-item" style="background: linear-gradient(135deg, #3B82F6, #1D4ED8);">
            <i class="fas fa-camera"></i>
          </div>
          <div class="gallery-item" style="background: linear-gradient(135deg, #8B5CF6, #7C3AED);">
            <i class="fas fa-graduation-cap"></i>
          </div>
          <div class="gallery-item" style="background: linear-gradient(135deg, #10B981, #059669);">
            <i class="fas fa-laptop-code"></i>
          </div>
          <div class="gallery-item" style="background: linear-gradient(135deg, #F59E0B, #D97706);">
            <i class="fas fa-trophy"></i>
          </div>
          <div class="gallery-item" style="background: linear-gradient(135deg, #6366F1, #4F46E5);">
            <i class="fas fa-handshake"></i>
          </div>
          <div class="gallery-item" style="background: linear-gradient(135deg, #EC4899, #DB2777);">
            <i class="fas fa-rocket"></i>
          </div>
        </div>

        <p class="gallery-notice text-center content-section" data-aos="fade-up">
          Gallery akan segera hadir dengan dokumentasi kegiatan terbaru
        </p>
      </div>
    </section>

    <!-- Footer -->
    <footer class="footer bg-gray-800 text-white text-center py-6 mt-auto">
      <p class="footer-text">&copy; 2025 HIMATIF Universitas Bengkulu</p>
    </footer>
  </div>
</template>

<style>
body {
  background: #0f172a;
  color: #f3f4f6;
  overflow-x: hidden;
}

/* Navbar Styles */
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

.mobile-menu-btn {
  display: none;
  background: none;
  border: none;
  color: #e5e7eb;
  font-size: 1.5rem;
  cursor: pointer;
}

/* Hero Section */
.hero {
  min-height: 100vh;
  background: linear-gradient(-45deg, #0f172a, #1e293b, #0c4a6e, #1e3a8a);
  background-size: 400% 400%;
  animation: gradient-shift 15s ease infinite;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  overflow: hidden;
  padding: 6rem 1.5rem 2rem;
}

.hero::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(to bottom, transparent, rgba(17, 24, 39, 0.7));
}

.hero-content {
  max-width: 1000px;
  text-align: center;
  position: relative;
  z-index: 2;
}

.hero-badge {
  background: rgba(96, 165, 250, 0.2);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(96, 165, 250, 0.3);
  border-radius: 50px;
  padding: 0.75rem 1.5rem;
  display: inline-block;
  margin-bottom: 2rem;
}

.hero-badge span {
  color: #60a5fa;
  font-weight: 600;
  font-size: 1.1rem;
}

.hero-title {
  font-size: 4rem;
  font-weight: 900;
  margin-bottom: 1.5rem;
  line-height: 1.1;
}

.gradient-text {
  background: linear-gradient(135deg, #60a5fa, #3b82f6, #1d4ed8);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.hero-description {
  font-size: 1.4rem;
  color: #d1d5db;
  line-height: 1.6;
  max-width: 800px;
  margin: 0 auto 3rem;
}

.scroll-indicator {
  position: absolute;
  bottom: 2rem;
  left: 50%;
  transform: translateX(-50%);
  animation: bounce 2s infinite;
}

.scroll-circle {
  width: 30px;
  height: 50px;
  border: 2px solid #60a5fa;
  border-radius: 25px;
  display: flex;
  justify-content: center;
}

.scroll-dot {
  width: 4px;
  height: 10px;
  background: #60a5fa;
  border-radius: 2px;
  margin-top: 10px;
  animation: scroll-dot 2s infinite;
}

/* Main Content */
.section {
  padding: 5rem 1.5rem;
  position: relative;
}

.section-container {
  max-width: 1200px;
  margin: 0 auto;
}

.section-title {
  text-align: center;
  margin-bottom: 4rem;
}

.section-title h2 {
  font-size: 3.5rem;
  font-weight: 800;
  margin-bottom: 1rem;
}

.section-title p {
  font-size: 1.25rem;
  color: #9ca3af;
  max-width: 600px;
  margin: 0 auto;
}

/* About Section */
.about-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
  margin-bottom: 5rem;
}

.about-content h2 {
  font-size: 3rem;
  font-weight: 800;
  margin-bottom: 2rem;
}

.about-text {
  font-size: 1.1rem;
  line-height: 1.7;
  color: #d1d5db;
}

.about-text p {
  margin-bottom: 1.5rem;
}

.about-visual {
  display: flex;
  justify-content: center;
}

.logo-visual {
  position: relative;
  width: 350px;
  height: 350px;
}

.logo-glow {
  position: absolute;
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, #3b82f6, #6366f1);
  border-radius: 50%;
  filter: blur(40px);
  opacity: 0.3;
  animation: pulse-glow 3s infinite;
}

.logo-main {
  position: relative;
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, #3b82f6, #6366f1);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 20px 40px rgba(59, 130, 246, 0.3);
  animation: float 6s ease-in-out infinite;
}

.logo-main span {
  font-size: 2.5rem;
  font-weight: 800;
  color: white;
}

/* Stats Section */
.stats-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 2rem;
  margin-bottom: 5rem;
}

.stat-card {
  background: rgba(31, 41, 55, 0.7);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(55, 65, 81, 0.5);
  border-radius: 1.5rem;
  padding: 2rem;
  text-align: center;
  transition: all 0.3s ease;
}

.stat-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 20px 40px rgba(59, 130, 246, 0.2);
  border-color: rgba(59, 130, 246, 0.5);
}

.stat-number {
  font-size: 3.5rem;
  font-weight: 800;
  margin-bottom: 0.5rem;
  background: linear-gradient(135deg, #60a5fa, #3b82f6);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.stat-label {
  color: #9ca3af;
  font-size: 1rem;
}

/* Vision & Mission */
.vm-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2rem;
  margin-bottom: 5rem;
}

.vm-card {
  background: rgba(31, 41, 55, 0.7);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(55, 65, 81, 0.5);
  border-radius: 1.5rem;
  padding: 2.5rem;
  transition: all 0.3s ease;
}

.vm-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 20px 40px rgba(59, 130, 246, 0.2);
  border-color: rgba(59, 130, 246, 0.5);
}

.vm-header {
  display: flex;
  align-items: center;
  margin-bottom: 2rem;
}

.vm-icon {
  width: 70px;
  height: 70px;
  border-radius: 1rem;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-right: 1.5rem;
  font-size: 2rem;
}

.vision .vm-icon {
  background: linear-gradient(135deg, #3b82f6, #1d4ed8);
}

.mission .vm-icon {
  background: linear-gradient(135deg, #8b5cf6, #7c3aed);
}

.vm-title {
  font-size: 1.8rem;
  font-weight: 700;
}

.vm-content {
  color: #d1d5db;
  line-height: 1.7;
  font-size: 1.1rem;
}

/* Leadership */
.leadership-content {
  background: rgba(31, 41, 55, 0.7);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(55, 65, 81, 0.5);
  border-radius: 1.5rem;
  padding: 3rem;
  text-align: center;
  margin-bottom: 3rem;
}

.leadership-text {
  font-size: 1.1rem;
  line-height: 1.7;
  color: #d1d5db;
  margin-bottom: 2rem;
  max-width: 900px;
  margin-left: auto;
  margin-right: auto;
}

.motto-box {
  background: linear-gradient(135deg, rgba(59, 130, 246, 0.2), rgba(139, 92, 246, 0.2));
  border-radius: 1rem;
  padding: 2rem;
  margin-top: 2rem;
  display: inline-block;
}

.motto {
  font-size: 2rem;
  font-weight: 700;
  margin-bottom: 0.5rem;
}

.motto-label {
  color: #9ca3af;
  font-style: italic;
}

/* Logo Philosophy */
.philosophy-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 3rem;
  align-items: center;
  margin-bottom: 5rem;
}

.philosophy-content {
  background: rgba(31, 41, 55, 0.7);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(55, 65, 81, 0.5);
  border-radius: 1.5rem;
  padding: 2.5rem;
}

.philosophy-text {
  font-size: 1.1rem;
  line-height: 1.7;
  color: #d1d5db;
  margin-bottom: 2rem;
}

.meaning-item {
  display: flex;
  align-items: flex-start;
  gap: 1rem;
  margin-bottom: 1.5rem;
}

.meaning-number {
  min-width: 35px;
  height: 35px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 700;
  color: white;
  font-size: 0.9rem;
}

.meaning-content h4 {
  font-size: 1.1rem;
  margin-bottom: 0.3rem;
}

.meaning-content p {
  color: #9ca3af;
  font-size: 0.95rem;
}

.philosophy-visual {
  display: flex;
  justify-content: center;
}

/* Gallery */
.gallery-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.5rem;
  margin-bottom: 2rem;
}

.gallery-item {
  aspect-ratio: 1;
  border-radius: 1rem;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 2rem;
  opacity: 0.7;
  transition: all 0.3s ease;
}

.gallery-item:hover {
  opacity: 1;
  transform: scale(1.05);
}

.gallery-notice {
  color: #9ca3af;
  font-size: 1.1rem;
}

/* Footer */
.footer {
  background: #111827;
  padding: 3rem 1.5rem;
  text-align: center;
}

.footer-text {
  color: #9ca3af;
}

/* Animations */
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

@keyframes bounce {

  0%,
  20%,
  50%,
  80%,
  100% {
    transform: translateY(0) translateX(-50%);
  }

  40% {
    transform: translateY(-20px) translateX(-50%);
  }

  60% {
    transform: translateY(-10px) translateX(-50%);
  }
}

@keyframes scroll-dot {
  0% {
    opacity: 0;
    transform: translateY(0);
  }

  50% {
    opacity: 1;
  }

  100% {
    opacity: 0;
    transform: translateY(20px);
  }
}

@keyframes float {

  0%,
  100% {
    transform: translateY(0);
  }

  50% {
    transform: translateY(-15px);
  }
}

@keyframes pulse-glow {

  0%,
  100% {
    opacity: 0.3;
  }

  50% {
    opacity: 0.5;
  }
}

/* Responsive Design */
@media (max-width: 1024px) {
  .hero-title {
    font-size: 3rem;
  }

  .about-grid,
  .vm-grid,
  .philosophy-grid {
    grid-template-columns: 1fr;
    gap: 3rem;
  }

  .stats-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 768px) {
  .nav-links {
    display: none;
  }

  .mobile-menu-btn {
    display: block;
  }

  .hero-title {
    font-size: 2.5rem;
  }

  .hero-description {
    font-size: 1.1rem;
  }

  .section-title h2 {
    font-size: 2.5rem;
  }

  .stats-grid {
    grid-template-columns: 1fr;
  }

  .gallery-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 480px) {
  .logo-text {
    font-size: 1.2rem;
  }

  .hero-title {
    font-size: 2rem;
  }

  .section-title h2 {
    font-size: 2rem;
  }

  .gallery-grid {
    grid-template-columns: 1fr;
  }

  .vm-card,
  .philosophy-content {
    padding: 1.5rem;
  }
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }

  100% {
    transform: rotate(360deg);
  }
}

/* Efek transisi untuk konten */
.content-section {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.8s ease, transform 0.8s ease;
}

.content-section.visible {
  opacity: 1;
  transform: translateY(0);
}

/* Loading state untuk debugging */
.page-loading {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: #0f172a;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 9999;
}

.loading-spinner {
  width: 50px;
  height: 50px;
  border: 3px solid rgba(96, 165, 250, 0.3);
  border-top: 3px solid #60a5fa;
  border-radius: 50%;
  animation: spin 1s linear infinite;
}
</style>