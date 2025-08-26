<script setup>
import { Link } from '@inertiajs/vue3'
import { onMounted, nextTick, ref, onUnmounted } from 'vue'

// === State Umum ===
const activeTab = ref('vision-mission')
const isLoaded = ref(false)
const activeDepartment = ref(null)

const setActiveTab = (tab) => {
  activeTab.value = tab
}

const setActiveDepartment = (dept) => {
  activeDepartment.value = dept
}

// === Data Departemen + Anggota ===
const departments = [
  {
    name: 'Inti',
    icon: 'fas fa-star',
    description: 'Departemen inti yang mengelola koordinasi organisasi',
    members: [
      { name: 'Ketua Umum', position: 'Ketua', batch: '2023' },
      { name: 'Sekretaris', position: 'Sekretaris', batch: '2023' },
      { name: 'Bendahara', position: 'Bendahara', batch: '2023' }
    ]
  },
  {
    name: 'Akademik',
    icon: 'fas fa-graduation-cap',
    description: 'Mengembangkan program akademik dan peningkatan keilmuan',
    members: [
      { name: 'Koordinator Akademik', position: 'Koordinator', batch: '2023' },
      { name: 'Staff Akademik 1', position: 'Staff', batch: '2023' },
      { name: 'Staff Akademik 2', position: 'Staff', batch: '2023' }
    ]
  },
  {
    name: 'PSDM',
    icon: 'fas fa-users',
    description: 'Mengelola pengembangan sumber daya manusia',
    members: [
      { name: 'Koordinator PSDM', position: 'Koordinator', batch: '2023' },
      { name: 'Staff PSDM 1', position: 'Staff', batch: '2023' },
      { name: 'Staff PSDM 2', position: 'Staff', batch: '2023' }
    ]
  },
  {
    name: 'ADM',
    icon: 'fas fa-file-alt',
    description: 'Administrasi dan dokumentasi organisasi',
    members: [
      { name: 'Koordinator ADM', position: 'Koordinator', batch: '2023' },
      { name: 'Staff ADM 1', position: 'Staff', batch: '2023' }
    ]
  },
  {
    name: 'Kominfo',
    icon: 'fas fa-bullhorn',
    description: 'Komunikasi dan informasi internal/eksternal',
    members: [
      { name: 'Koordinator Kominfo', position: 'Koordinator', batch: '2023' },
      { name: 'Staff Kominfo 1', position: 'Staff', batch: '2023' },
      { name: 'Staff Kominfo 2', position: 'Staff', batch: '2023' }
    ]
  },
  {
    name: 'PMB',
    icon: 'fas fa-user-plus',
    description: 'Pengelolaan mahasiswa baru',
    members: [
      { name: 'Koordinator PMB', position: 'Koordinator', batch: '2023' },
      { name: 'Staff PMB 1', position: 'Staff', batch: '2023' }
    ]
  },
  {
    name: 'KWU',
    icon: 'fas fa-coins',
    description: 'Kewirausahaan dan pengembangan usaha',
    members: [
      { name: 'Koordinator KWU', position: 'Koordinator', batch: '2023' },
      { name: 'Staff KWU 1', position: 'Staff', batch: '2023' },
      { name: 'Staff KWU 2', position: 'Staff', batch: '2023' }
    ]
  },
  {
    name: 'Kastrad',
    icon: 'fas fa-balance-scale',
    description: 'Kajian dan strategi organisasi',
    members: [
      { name: 'Koordinator Kastrad', position: 'Koordinator', batch: '2023' },
      { name: 'Staff Kastrad 1', position: 'Staff', batch: '2023' }
    ]
  }
]

// === Data Anggota Inti / Showcase (opsional) ===
const members = [
  { name: 'Putri Alisya Zhafirah', position: 'Bendahara Umum II', batch: 'BIL A 2023', image: './img/member1.jpg' },
  { name: 'Muhammad Fattahul Aziz', position: 'Ketua Himpunan', batch: 'BIL 2023', image: './img/member2.jpg' },
  { name: 'Adhia Rihal Sulaiman', position: 'Wakil Ketua Himpunan', batch: 'REG A 2023', image: './img/member3.jpg' },
  { name: 'Azka Hukma Tsabita', position: 'Sekretaris Umum I', batch: 'BIL A 2023', image: './img/member4.jpg' },
]

// === Import dinamis AOS + PureCounter ===
let AOS = null
let PureCounter = null

// Variables for cleanup
let scrollHandler = null
let observer = null

const initializeLibraries = async () => {
  try {
    const aosModule = await import('aos')
    AOS = aosModule.default
    await import('aos/dist/aos.css')

    const pureCounterModule = await import('@srexi/purecounterjs')
    PureCounter = pureCounterModule.default
    return true
  } catch (error) {
    console.warn('Failed to load libraries:', error)
    return false
  }
}

const setupAnimations = () => {
  if (!AOS) return
  AOS.init({
    duration: 1000,
    easing: 'ease-out-cubic',
    once: true,
    offset: 100,
  })
}

const setupPureCounter = () => {
  if (!PureCounter) return
  try {
    setTimeout(() => {
      new PureCounter({
        duration: 2,
        delay: 10,
        once: true
      })
    }, 500)
  } catch (error) {
    console.warn('PureCounter initialization failed:', error)
  }
}

const setupScrollEffects = () => {
  if (typeof document !== 'undefined') {
    document.documentElement.style.scrollBehavior = 'smooth'
  }

  scrollHandler = () => {
    const navbar = document.querySelector('.navbar')
    if (navbar) {
      if (window.scrollY > 50) {
        navbar.classList.add('scrolled')
      } else {
        navbar.classList.remove('scrolled')
      }
    }
  }

  if (typeof window !== 'undefined') {
    window.addEventListener('scroll', scrollHandler)
  }
}

const setupIntersectionObserver = () => {
  if (typeof window === 'undefined' || typeof IntersectionObserver === 'undefined') return

  const sections = document.querySelectorAll('section')
  const observerOptions = {
    threshold: 0.1,
    rootMargin: '0px 0px -50px 0px',
  }

  observer = new IntersectionObserver((entries) => {
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
}

const setupActiveNavLinks = () => {
  if (typeof window === 'undefined') return
  const links = document.querySelectorAll('.nav-link')
  const currentPath = window.location.pathname
  links.forEach(link => {
    if (link.getAttribute('href') === currentPath) {
      link.classList.add('active')
    }
  })
}

onMounted(async () => {
  if (typeof window === 'undefined') return
  await nextTick()

  const librariesLoaded = await initializeLibraries()
  if (librariesLoaded) {
    setupAnimations()
    setupPureCounter()
  }

  setupScrollEffects()
  setupIntersectionObserver()
  setupActiveNavLinks()

  setTimeout(() => {
    isLoaded.value = true
  }, 100)
})

onUnmounted(() => {
  if (scrollHandler && typeof window !== 'undefined') {
    window.removeEventListener('scroll', scrollHandler)
  }
  if (observer) {
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

    <!-- Main Content -->
    <main class="bg-gradient-to-b from-gray-900 via-[#0d0d1a] to-gray-950 text-gray-200 min-h-screen pt-24">
      <!-- Hero Section -->
      <section class="text-center py-16 relative overflow-hidden">
        <p class="text-blue-400 font-semibold mb-4">Our Team</p>
        <h1
          class="text-4xl md:text-5xl font-bold bg-gradient-to-r from-blue-400 to-purple-400 bg-clip-text text-transparent">
          Our Strength Lies In Our Team
        </h1>
        <p class="mt-4 text-gray-400 max-w-2xl mx-auto">
          Kami persembahkan jajaran kabinet HMIF yang penuh semangat!
          Bersama, kita kuatkan formasi dan wujudkan inovasi!
        </p>
        <div class="mt-10">
          <a href="#departments" class="inline-flex justify-center">
            <div
              class="w-12 h-12 rounded-full border border-gray-600 flex items-center justify-center text-gray-400 hover:text-blue-400 hover:border-blue-400 transition">
              <i class="fas fa-chevron-down"></i>
            </div>
          </a>
        </div>
      </section>

      <!-- Departments Section -->
      <section id="departments" class="py-20">
        <div class="text-center mb-12">
          <p class="text-purple-400 font-semibold mb-2">Explore</p>
          <h2
            class="text-3xl md:text-4xl font-bold bg-gradient-to-r from-blue-400 to-purple-400 bg-clip-text text-transparent">
            Our Cabinet
          </h2>
        </div>

        <!-- Grid Departments -->
        <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 gap-8 max-w-5xl mx-auto px-6">
          <div v-for="(dept, i) in departments" :key="i" @click="setActiveDepartment(dept)"
            class="cursor-pointer bg-gray-800/40 hover:bg-gray-800 rounded-2xl p-6 shadow-lg border border-gray-700 hover:border-blue-500/50 text-center transition-all hover:shadow-blue-500/20">
            <div class="text-4xl mb-4 text-blue-400">
              <i :class="dept.icon"></i>
            </div>
            <h3 class="text-lg font-semibold text-white">{{ dept.name }}</h3>
            <p class="text-sm text-gray-400">{{ dept.description }}</p>
          </div>
        </div>

        <!-- Members of selected department -->
        <div v-if="activeDepartment" class="mt-16 max-w-4xl mx-auto">
          <h3 class="text-2xl font-bold text-center text-blue-400 mb-8">
            Anggota {{ activeDepartment.name }}
          </h3>
          <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-8">
            <div v-for="(member, idx) in activeDepartment.members" :key="idx"
              class="bg-gray-800/40 rounded-xl p-6 shadow-lg border border-gray-700 hover:border-purple-500/50 transition-all">
              <h4 class="text-white font-semibold">{{ member.name }}</h4>
              <p class="text-blue-400 text-sm">{{ member.position }}</p>
              <p class="text-gray-400 text-xs mt-1">{{ member.batch }}</p>
            </div>
          </div>
        </div>
      </section>
    </main>

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
        <div class="footer-divider border-t border-gray-700"></div>

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
  height: 2px;
  background: #60a5fa;
}

.nav-link.active {
  color: #60a5fa;
}

.mobile-menu-btn {
  display: none;
  background: none;
  border: none;
  color: #e5e7eb;
  font-size: 1.5rem;
  cursor: pointer;
}

/* Hero Section Styles */
.hero-section {
  background: linear-gradient(135deg, #0f172a 0%, #1e293b 50%, #0f172a 100%);
  position: relative;
}

.hero-section::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-image: radial-gradient(circle at 20% 50%, rgba(59, 130, 246, 0.1) 0%, transparent 50%),
    radial-gradient(circle at 80% 20%, rgba(139, 92, 246, 0.1) 0%, transparent 50%),
    radial-gradient(circle at 40% 80%, rgba(16, 185, 129, 0.1) 0%, transparent 50%);
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

.floating-element {
  animation: floatUpDown 4s ease-in-out infinite;
}

@keyframes floatUpDown {

  0%,
  100% {
    transform: translateY(0px);
  }

  50% {
    transform: translateY(-30px);
  }
}

/* Button Styles */
.btn-primary {
  background: linear-gradient(135deg, #3b82f6, #8b5cf6);
  color: white;
  border: none;
  transition: all 0.3s ease;
}

.btn-primary:hover {
  background: linear-gradient(135deg, #2563eb, #7c3aed);
  box-shadow: 0 10px 30px rgba(59, 130, 246, 0.3);
}

.btn-secondary {
  background: transparent;
  transition: all 0.3s ease;
}

/* Newsletter Styles */
.newsletter-input {
  background: #374151;
  border: 1px solid #4b5563;
  color: #f3f4f6;
}

.newsletter-btn {
  background: linear-gradient(135deg, #3b82f6, #8b5cf6);
  transition: all 0.3s ease;
}

.newsletter-btn:hover {
  background: linear-gradient(135deg, #2563eb, #7c3aed);
  transform: translateY(-2px);
}

/* Social Icons */
.social-icon {
  transition: all 0.3s ease;
}

.social-icon:hover {
  transform: translateY(-3px);
}

.footer-link {
  transition: all 0.2s ease;
}

.footer-link:hover {
  color: #3b82f6;
  transform: translateX(5px);
}

.footer-divider {
  border-top: 1px solid rgba(100, 116, 139, 0.3);
  margin: 2rem 0;
}

/* Custom Scrollbar */
::-webkit-scrollbar {
  width: 8px;
}

::-webkit-scrollbar-track {
  background: #1f2937;
}

::-webkit-scrollbar-thumb {
  background: linear-gradient(135deg, #3b82f6, #8b5cf6);
  border-radius: 4px;
}

::-webkit-scrollbar-thumb:hover {
  background: linear-gradient(135deg, #2563eb, #7c3aed);
}

/* Responsive Design */
@media (max-width: 768px) {
  .nav-links {
    display: none;
  }

  .mobile-menu-btn {
    display: block;
  }

  .logo-text {
    font-size: 1.2rem;
  }

  .hero-section h1 {
    font-size: 2.5rem;
  }

  .hero-section p {
    font-size: 1.1rem;
  }
}

/* Tab Animation */
.tab-content {
  animation: fadeInUp 0.6s ease-out;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Card Hover Effects */
.hover\\:scale-105:hover {
  transform: scale(1.05);
}

.transition-all {
  transition: all 0.3s ease;
}

/* Gradient Text */
.bg-clip-text {
  -webkit-background-clip: text;
  background-clip: text;
}

/* Glass Effect */
.backdrop-blur-md {
  backdrop-filter: blur(12px);
}

/* Custom Color Classes for Dynamic Styling */
.bg-blue-500\/20 {
  background-color: rgba(59, 130, 246, 0.2);
}

.bg-purple-500\/20 {
  background-color: rgba(139, 92, 246, 0.2);
}

.bg-green-500\/20 {
  background-color: rgba(34, 197, 94, 0.2);
}

.bg-yellow-500\/20 {
  background-color: rgba(234, 179, 8, 0.2);
}

.text-blue-400 {
  color: #60a5fa;
}

.text-purple-400 {
  color: #a78bfa;
}

.text-green-400 {
  color: #4ade80;
}

.text-yellow-400 {
  color: #facc15;
}
</style>