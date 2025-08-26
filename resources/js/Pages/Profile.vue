<script setup>
import { Link } from '@inertiajs/vue3'
import AOS from 'aos'
import 'aos/dist/aos.css'
import { onMounted, nextTick } from 'vue'
import PureCounter from '@srexi/purecounterjs'

onMounted(async () => {
  await nextTick()

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

  // ✅ Smooth scroll
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

  // ✅ Intersection Observer (animasi section saat muncul)
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

  // ✅ Highlight active nav-link
  const links = document.querySelectorAll('.nav-link')
  const currentPath = window.location.pathname
  links.forEach(link => {
    if (link.getAttribute('href') === currentPath) {
      link.classList.add('active')
    }
  })

  // Cleanup ketika komponen unmounted
  return () => {
    window.removeEventListener('scroll', handleScroll)
    observer.disconnect()
  }
})
</script>

<template>
    <div class="min-h-screen flex flex-col">
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
            <Link href="/" class="nav-link" :class="{ 'active': route().current('home') }">Home</Link>
          </li>
          <li>
            <Link href="/about" class="nav-link" :class="{ 'active': route().current('about') }">About Us</Link>
          </li>
          <li>
            <Link href="/profiles" class="nav-link" :class="{ 'active': route().current('profiles') }">Profile</Link>
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

    <!-- Footer -->
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
</style>