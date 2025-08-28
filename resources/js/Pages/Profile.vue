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

// Handle image loading errors
const handleImageError = (event) => {
  event.target.style.display = 'none'
  const placeholder = event.target.parentNode.querySelector('.avatar-placeholder') ||
    document.createElement('div')

  if (!event.target.parentNode.querySelector('.avatar-placeholder')) {
    placeholder.className = 'avatar-placeholder'
    placeholder.innerHTML = '<i class="fas fa-user"></i>'
    event.target.parentNode.appendChild(placeholder)
  }
}

// === Data Departemen + Anggota ===
const departments = [
  {
    name: 'Inti',
    icon: 'fas fa-star',
    color: 'from-yellow-400 to-orange-500',
    bgColor: 'bg-yellow-500/20',
    borderColor: 'border-yellow-500/50',
    description: 'Kepemimpinan utama yang mengatur koordinasi dan kebijakan organisasi',
    members: [
      {
        name: 'Muhammad Fattahul Aziz',
        position: 'Ketua Umum',
        batch: '2023',
        instagram: 'https://instagram.com/fattahul.aziz',
        email: 'ketua@himatif.unib.ac.id',
        photo: './img/members/fattahul-aziz.jpg'
      },
      {
        name: 'Azka Hukma Tsabita',
        position: 'Sekretaris Umum',
        batch: '2023',
        instagram: 'https://instagram.com/azka.hukma',
        email: 'sekretaris@himatif.unib.ac.id',
        photo: './img/members/azka-hukma.jpg'
      },
      {
        name: 'Putri Alisya Zhafirah',
        position: 'Bendahara Umum',
        batch: '2023',
        instagram: 'https://instagram.com/putri.alisya',
        email: 'bendahara@himatif.unib.ac.id',
        photo: './img/members/putri-alisya.jpg'
      }
    ]
  },
  {
    name: 'PSDM',
    icon: 'fas fa-users',
    color: 'from-green-400 to-emerald-500',
    bgColor: 'bg-green-500/20',
    borderColor: 'border-green-500/50',
    description: 'Pengembangan Sumber Daya Manusia untuk kaderisasi dan pelatihan anggota',
    members: [
      {
        name: 'Reza Fahlevi Rahman',
        position: 'Koordinator PSDM',
        batch: '2023',
        instagram: 'https://instagram.com/reza.fahlevi',
        email: 'psdm.koordinator@himatif.unib.ac.id',
        photo: './img/members/reza-fahlevi.jpg'
      },
      {
        name: 'Maya Sari Dewi',
        position: 'Staff PSDM',
        batch: '2023',
        instagram: 'https://instagram.com/maya.saridewi',
        email: 'psdm.staff1@himatif.unib.ac.id',
        photo: './img/members/maya-sari.jpg'
      },
      {
        name: 'Andi Kurniawan',
        position: 'Staff PSDM',
        batch: '2023',
        instagram: 'https://instagram.com/andi.kurniawan',
        email: 'psdm.staff2@himatif.unib.ac.id',
        photo: './img/members/andi-kurniawan.jpg'
      }
    ]
  },
  {
    name: 'Kominfo',
    icon: 'fas fa-bullhorn',
    color: 'from-pink-400 to-rose-500',
    bgColor: 'bg-pink-500/20',
    borderColor: 'border-pink-500/50',
    description: 'Komunikasi, informasi, publikasi, dan pengembangan teknologi digital',
    members: [
      {
        name: 'Akhmat Qavidhufahmi',
        position: 'Kepala Departemen',
        batch: '2023',
        instagram: 'https://instagram.com/farel.satria',
        email: 'kominfo.koordinator@himatif.unib.ac.id',
        photo: './img/Akhmat.jpeg'
      },
      {
        name: 'Aulia Dwi Rahmadan',
        position: 'Sekretaris Departemen',
        batch: '2023',
        instagram: 'https://instagram.com/alya.cantika',
        email: 'kominfo.staff1@himatif.unib.ac.id',
        photo: './img/members/alya-cantika.jpg'
      },
      {
        name: 'Khaylilla Shafaraly',
        position: 'Bendahara Departemen',
        batch: '2023',
        instagram: 'https://instagram.com/rio.ferdinan',
        email: 'kominfo.staff2@himatif.unib.ac.id',
        photo: './img/members/rio-ferdinan.jpg'
      },
      {
        name: 'Muhammad Sahlan Habibi',
        position: 'Kepala Divisi PDD',
        batch: '2023',
        instagram: 'https://instagram.com/rio.ferdinan',
        email: 'kominfo.staff2@himatif.unib.ac.id',
        photo: './img/members/rio-ferdinan.jpg'
      },
      {
        name: 'Siddiq Bagus Firmansyah',
        position: 'Kepala Divisi RISTEK',
        batch: '2023',
        instagram: 'https://instagram.com/rio.ferdinan',
        email: 'kominfo.staff2@himatif.unib.ac.id',
        photo: './img/members/rio-ferdinan.jpg'
      }
    ]
  },
  {
    name: 'Kerohanian',
    icon: 'fas fa-file-alt',
    color: 'from-purple-400 to-violet-500',
    bgColor: 'bg-purple-500/20',
    borderColor: 'border-purple-500/50',
    description: 'Pembinaan spiritual dan keagamaan untuk memperkuat nilai-nilai keimanan',
    members: [
      {
        name: 'Indira Putri Maharani',
        position: 'Koordinator ADM',
        batch: '2023',
        instagram: 'https://instagram.com/indira.putri',
        email: 'adm.koordinator@himatif.unib.ac.id',
        photo: './img/members/indira-putri.jpg'
      },
      {
        name: 'Bayu Pratama Wijaya',
        position: 'Staff ADM',
        batch: '2023',
        instagram: 'https://instagram.com/bayu.pratama',
        email: 'adm.staff@himatif.unib.ac.id',
        photo: './img/members/bayu-pratama.jpg'
      }
    ]
  },
  {
    name: 'Humas',
    icon: 'fas fa-user-plus',
    color: 'from-indigo-400 to-blue-600',
    bgColor: 'bg-indigo-500/20',
    borderColor: 'border-indigo-500/50',
    description: 'Hubungan Masyarakat untuk menjalin kemitraan eksternal dan networking',
    members: [
      {
        name: 'Tasya Amelia Putri',
        position: 'Koordinator PMB',
        batch: '2023',
        instagram: 'https://instagram.com/tasya.amelia',
        email: 'pmb.koordinator@himatif.unib.ac.id',
        photo: './img/members/tasya-amelia.jpg'
      },
      {
        name: 'Rangga Adi Putra',
        position: 'Staff PMB',
        batch: '2023',
        instagram: 'https://instagram.com/rangga.adiputra',
        email: 'pmb.staff@himatif.unib.ac.id',
        photo: './img/members/rangga-adi.jpg'
      }
    ]
  },
  {
    name: 'Danus',
    icon: 'fas fa-coins',
    color: 'from-amber-400 to-yellow-600',
    bgColor: 'bg-amber-500/20',
    borderColor: 'border-amber-500/50',
    description: 'Dana dan Usaha untuk penggalangan dana dan kegiatan kewirausahaan',
    members: [
      {
        name: 'Dian Purnama Sari',
        position: 'Koordinator KWU',
        batch: '2023',
        instagram: 'https://instagram.com/dian.purnama',
        email: 'kwu.koordinator@himatif.unib.ac.id',
        photo: './img/members/dian-purnama.jpg'
      },
      {
        name: 'Kevin Mahardika',
        position: 'Staff KWU',
        batch: '2023',
        instagram: 'https://instagram.com/kevin.mahardika',
        email: 'kwu.staff1@himatif.unib.ac.id',
        photo: './img/members/kevin-mahardika.jpg'
      },
      {
        name: 'Sari Wulandari',
        position: 'Staff KWU',
        batch: '2023',
        instagram: 'https://instagram.com/sari.wulandari',
        email: 'kwu.staff2@himatif.unib.ac.id',
        photo: './img/members/sari-wulandari.jpg'
      }
    ]
  },
  {
    name: 'Minbak',
    icon: 'fas fa-balance-scale',
    color: 'from-teal-400 to-cyan-600',
    bgColor: 'bg-teal-500/20',
    borderColor: 'border-teal-500/50',
    description: 'Minat dan Bakat untuk mengembangkan potensi non-akademik mahasiswa',
    members: [
      {
        name: 'Fajar Ramadhan',
        position: 'Koordinator Kastrad',
        batch: '2023',
        instagram: 'https://instagram.com/fajar.ramadhan',
        email: 'kastrad.koordinator@himatif.unib.ac.id',
        photo: './img/members/fajar-ramadhan.jpg'
      },
      {
        name: 'Lina Marlina',
        position: 'Staff Kastrad',
        batch: '2023',
        instagram: 'https://instagram.com/lina.marlina',
        email: 'kastrad.staff@himatif.unib.ac.id',
        photo: './img/members/lina-marlina.jpg'
      }
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
    <main
      class="bg-gradient-to-b from-gray-900 via-[#0d0d1a] to-gray-950 text-gray-200 min-h-screen pt-24 relative overflow-hidden">
      <!-- Animated Background Elements -->
      <div class="absolute inset-0 overflow-hidden pointer-events-none">
        <div class="floating-orb orb-1"></div>
        <div class="floating-orb orb-2"></div>
        <div class="floating-orb orb-3"></div>
        <div class="floating-orb orb-4"></div>
        <div class="floating-particles"></div>
      </div>

      <!-- Hero Section -->
      <section class="text-center py-20 relative overflow-hidden">
        <div class="hero-glow"></div>
        <div class="relative z-10" data-aos="fade-up" data-aos-duration="800">
          <div class="inline-block mb-6">
            <span
              class="inline-flex items-center px-4 py-2 rounded-full bg-gradient-to-r from-blue-500/20 to-purple-500/20 border border-blue-500/30 text-blue-400 font-semibold text-sm backdrop-blur-sm">
              <i class="fas fa-users mr-2"></i>
              Our Amazing Team
            </span>
          </div>
          <h1 class="text-5xl md:text-7xl font-black mb-6 leading-tight">
            <span
              class="hero-title-animated bg-gradient-to-r from-blue-400 via-purple-400 to-cyan-400 bg-clip-text text-transparent">
              Our Strength Lies
            </span>
            <br>
            <span
              class="hero-title-animated bg-gradient-to-r from-purple-400 via-pink-400 to-blue-400 bg-clip-text text-transparent"
              style="animation-delay: 0.2s">
              In Our Team
            </span>
          </h1>
          <p class="mt-8 text-xl text-gray-300 max-w-3xl mx-auto leading-relaxed" data-aos="fade-up"
            data-aos-delay="200">
            Kami persembahkan jajaran kabinet <span class="text-blue-400 font-semibold">HMIF</span> yang penuh
            semangat!<br>
            Bersama, kita kuatkan formasi dan wujudkan inovasi untuk masa depan yang gemilang!
          </p>

          <!-- Statistics Cards -->
          <div class="grid grid-cols-2 md:grid-cols-4 gap-6 max-w-4xl mx-auto mt-16" data-aos="fade-up"
            data-aos-delay="400">
            <div class="stats-card group">
              <div class="stats-icon">
                <i class="fas fa-users"></i>
              </div>
              <h3 class="text-2xl font-bold text-white mb-1">{{ departments.length }}</h3>
              <p class="text-gray-400 text-sm">Departemen</p>
            </div>
            <div class="stats-card group">
              <div class="stats-icon">
                <i class="fas fa-user-tie"></i>
              </div>
              <h3 class="text-2xl font-bold text-white mb-1">20+</h3>
              <p class="text-gray-400 text-sm">Anggota Aktif</p>
            </div>
            <div class="stats-card group">
              <div class="stats-icon">
                <i class="fas fa-trophy"></i>
              </div>
              <h3 class="text-2xl font-bold text-white mb-1">15+</h3>
              <p class="text-gray-400 text-sm">Program Kerja</p>
            </div>
            <div class="stats-card group">
              <div class="stats-icon">
                <i class="fas fa-heart"></i>
              </div>
              <h3 class="text-2xl font-bold text-white mb-1">1</h3>
              <p class="text-gray-400 text-sm">Visi Bersama</p>
            </div>
          </div>

          <!-- Scroll Indicator -->
          <div class="mt-16" data-aos="fade-up" data-aos-delay="600">
            <a href="#departments" class="inline-flex justify-center scroll-indicator">
              <div class="pulse-ring"></div>
              <div class="scroll-arrow">
                <i class="fas fa-chevron-down"></i>
              </div>
            </a>
          </div>
        </div>
      </section>

      <!-- Departments Section -->
      <section id="departments" class="py-24 relative">
        <div class="text-center mb-16" data-aos="fade-up">
          <div class="inline-block mb-4">
            <span
              class="inline-flex items-center px-4 py-2 rounded-full bg-gradient-to-r from-purple-500/20 to-pink-500/20 border border-purple-500/30 text-purple-400 font-semibold text-sm backdrop-blur-sm">
              <i class="fas fa-sitemap mr-2"></i>
              Explore Our Structure
            </span>
          </div>
          <h2 class="text-4xl md:text-6xl font-black mb-6">
            <span class="bg-gradient-to-r from-blue-400 to-purple-400 bg-clip-text text-transparent">
              Our Cabinet
            </span>
          </h2>
          <p class="text-xl text-gray-300 max-w-2xl mx-auto">
            Setiap departemen memiliki peran unik dalam membangun ekosistem HIMATIF yang solid dan inovatif
          </p>
        </div>

        <!-- Grid Departments -->
        <div class="max-w-6xl mx-auto px-6">
          <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 gap-6" data-aos="fade-up" data-aos-delay="200">
            <div v-for="(dept, i) in departments" :key="i" @click="setActiveDepartment(dept)"
              class="dept-card group cursor-pointer" :class="[dept.bgColor, dept.borderColor]" :data-aos-delay="i * 100"
              data-aos="zoom-in">
              <div class="dept-card-content">
                <div class="dept-icon-wrapper">
                  <div class="dept-icon" :class="`bg-gradient-to-r ${dept.color}`">
                    <i :class="dept.icon"></i>
                  </div>
                  <div class="dept-icon-glow" :class="`bg-gradient-to-r ${dept.color}`"></div>
                </div>
                <h3 class="text-lg font-bold text-white mb-2 group-hover:text-blue-400 transition-colors">{{ dept.name
                  }}</h3>
                <p class="text-sm text-gray-400 leading-relaxed">{{ dept.description }}</p>

                <!-- Member count badge -->
                <div
                  class="absolute top-4 right-4 bg-gray-800/80 backdrop-blur-sm rounded-full px-2 py-1 text-xs text-gray-300">
                  {{ dept.members.length }}
                </div>

                <!-- Hover effect overlay -->
                <div class="dept-overlay" :class="`bg-gradient-to-r ${dept.color}`"></div>
              </div>
            </div>
          </div>
        </div>

        <!-- Members of selected department -->
        <Transition name="fade-slide" mode="out-in">
          <div v-if="activeDepartment" class="mt-20 max-w-5xl mx-auto px-6">
            <div class="text-center mb-12" data-aos="fade-up">
              <h3 class="text-3xl font-bold mb-4">
                <span class="bg-gradient-to-r from-blue-400 to-purple-400 bg-clip-text text-transparent">
                  Tim {{ activeDepartment.name }}
                </span>
              </h3>
              <p class="text-gray-400">{{ activeDepartment.description }}</p>
            </div>

            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
              <div v-for="(member, idx) in activeDepartment.members" :key="idx" class="member-card group"
                data-aos="fade-up" :data-aos-delay="idx * 100">
                <div class="member-card-content">
                  <!-- Avatar placeholder -->
                  <div class="member-avatar">
                    <div class="avatar-image-wrapper">
                      <img v-if="member.photo" :src="member.photo" :alt="member.name" class="avatar-image"
                        @error="handleImageError" />
                      <div v-else class="avatar-placeholder">
                        <i class="fas fa-user"></i>
                      </div>
                    </div>
                    <div class="avatar-ring"></div>
                  </div>

                  <div class="member-info">
                    <h4 class="text-white font-bold text-lg mb-1">{{ member.name }}</h4>
                    <p class="text-blue-400 font-semibold text-sm mb-2">{{ member.position }}</p>
                    <p class="text-gray-400 text-xs mb-4">{{ member.batch }}</p>

                    <!-- Social Media Links -->
                    <div class="flex justify-center space-x-4">
                      <a :href="member.instagram" target="_blank" rel="noopener noreferrer"
                        class="social-btn instagram-btn group/social" title="Instagram">
                        <i class="fab fa-instagram"></i>
                      </a>
                      <a :href="`mailto:${member.email}`" class="social-btn email-btn group/social" title="Email">
                        <i class="fas fa-envelope"></i>
                      </a>
                    </div>
                  </div>

                  <!-- Background decoration -->
                  <div class="member-bg-decoration"></div>
                </div>
              </div>
            </div>

            <!-- Close button -->
            <div class="text-center mt-12">
              <button @click="setActiveDepartment(null)" class="close-btn group" data-aos="fade-up">
                <i class="fas fa-times mr-2"></i>
                Tutup Detail
              </button>
            </div>
          </div>
        </Transition>
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

/* Animated Background Elements */
.floating-orb {
  position: absolute;
  border-radius: 50%;
  filter: blur(40px);
  animation: floatOrb 15s ease-in-out infinite;
  pointer-events: none;
}

.orb-1 {
  width: 200px;
  height: 200px;
  background: radial-gradient(circle, rgba(59, 130, 246, 0.3) 0%, transparent 70%);
  top: 20%;
  left: 10%;
  animation-delay: 0s;
}

.orb-2 {
  width: 150px;
  height: 150px;
  background: radial-gradient(circle, rgba(139, 92, 246, 0.25) 0%, transparent 70%);
  top: 60%;
  right: 20%;
  animation-delay: -5s;
}

.orb-3 {
  width: 180px;
  height: 180px;
  background: radial-gradient(circle, rgba(236, 72, 153, 0.2) 0%, transparent 70%);
  bottom: 30%;
  left: 20%;
  animation-delay: -10s;
}

.orb-4 {
  width: 120px;
  height: 120px;
  background: radial-gradient(circle, rgba(34, 197, 94, 0.25) 0%, transparent 70%);
  top: 40%;
  right: 10%;
  animation-delay: -7s;
}

@keyframes floatOrb {

  0%,
  100% {
    transform: translateY(0px) translateX(0px) scale(1);
  }

  25% {
    transform: translateY(-20px) translateX(10px) scale(1.1);
  }

  50% {
    transform: translateY(-10px) translateX(-15px) scale(0.9);
  }

  75% {
    transform: translateY(-30px) translateX(5px) scale(1.05);
  }
}

.floating-particles {
  position: absolute;
  width: 100%;
  height: 100%;
  background-image:
    radial-gradient(2px 2px at 40px 60px, rgba(59, 130, 246, 0.4), transparent),
    radial-gradient(2px 2px at 90px 40px, rgba(139, 92, 246, 0.3), transparent),
    radial-gradient(1px 1px at 120px 80px, rgba(236, 72, 153, 0.4), transparent),
    radial-gradient(1px 1px at 180px 30px, rgba(34, 197, 94, 0.3), transparent);
  background-repeat: repeat;
  background-size: 200px 100px;
  animation: particleMove 20s linear infinite;
  opacity: 0.6;
}

@keyframes particleMove {
  0% {
    transform: translateY(0px);
  }

  100% {
    transform: translateY(-100px);
  }
}

/* Hero Section Styles */
.hero-glow {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 600px;
  height: 600px;
  background: radial-gradient(circle, rgba(59, 130, 246, 0.1) 0%, transparent 70%);
  filter: blur(100px);
  animation: pulseGlow 4s ease-in-out infinite alternate;
}

@keyframes pulseGlow {
  0% {
    transform: translate(-50%, -50%) scale(0.8);
    opacity: 0.5;
  }

  100% {
    transform: translate(-50%, -50%) scale(1.2);
    opacity: 0.8;
  }
}

.hero-title-animated {
  animation: titleSlideUp 1s ease-out forwards;
  opacity: 0;
  transform: translateY(30px);
}

@keyframes titleSlideUp {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Statistics Cards */
.stats-card {
  background: rgba(31, 41, 55, 0.5);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(75, 85, 99, 0.3);
  border-radius: 1rem;
  padding: 1.5rem;
  text-align: center;
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
}

.stats-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(59, 130, 246, 0.1), transparent);
  transition: left 0.5s;
}

.stats-card:hover::before {
  left: 100%;
}

.stats-card:hover {
  transform: translateY(-5px);
  border-color: rgba(59, 130, 246, 0.5);
  box-shadow: 0 20px 40px rgba(59, 130, 246, 0.1);
}

.stats-icon {
  width: 50px;
  height: 50px;
  margin: 0 auto 1rem;
  background: linear-gradient(135deg, #3b82f6, #8b5cf6);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-size: 1.2rem;
  transition: all 0.3s ease;
}

.stats-card:hover .stats-icon {
  transform: scale(1.1) rotate(5deg);
}

/* Scroll Indicator */
.scroll-indicator {
  position: relative;
}

.pulse-ring {
  width: 60px;
  height: 60px;
  border: 2px solid rgba(59, 130, 246, 0.3);
  border-radius: 50%;
  position: absolute;
  animation: pulseRing 2s cubic-bezier(0.455, 0.03, 0.515, 0.955) infinite;
}

@keyframes pulseRing {
  0% {
    transform: scale(0.8);
    opacity: 1;
  }

  100% {
    transform: scale(1.4);
    opacity: 0;
  }
}

.scroll-arrow {
  width: 48px;
  height: 48px;
  background: linear-gradient(135deg, #3b82f6, #8b5cf6);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  transition: all 0.3s ease;
  animation: bounce 2s infinite;
}

.scroll-arrow:hover {
  transform: scale(1.1);
}

@keyframes bounce {

  0%,
  20%,
  50%,
  80%,
  100% {
    transform: translateY(0);
  }

  40% {
    transform: translateY(-10px);
  }

  60% {
    transform: translateY(-5px);
  }
}

/* Department Cards */
.dept-card {
  background: rgba(31, 41, 55, 0.4);
  backdrop-filter: blur(10px);
  border: 1px solid;
  border-radius: 1.5rem;
  padding: 0;
  transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  position: relative;
  overflow: hidden;
  min-height: 220px;
}

.dept-card:hover {
  transform: translateY(-8px) scale(1.02);
  box-shadow: 0 25px 50px rgba(0, 0, 0, 0.3);
}

.dept-card-content {
  padding: 2rem;
  position: relative;
  z-index: 2;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

.dept-icon-wrapper {
  position: relative;
  margin-bottom: 1.5rem;
}

.dept-icon {
  width: 60px;
  height: 60px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.5rem;
  color: white;
  transition: all 0.4s ease;
  position: relative;
  z-index: 2;
}

.dept-icon-glow {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 80px;
  height: 80px;
  border-radius: 50%;
  opacity: 0;
  filter: blur(20px);
  transition: all 0.4s ease;
}

.dept-card:hover .dept-icon {
  transform: scale(1.1) rotate(5deg);
}

.dept-card:hover .dept-icon-glow {
  opacity: 0.6;
  transform: translate(-50%, -50%) scale(1.2);
}

.dept-overlay {
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  opacity: 0.1;
  transition: all 0.4s ease;
  z-index: 1;
}

.dept-card:hover .dept-overlay {
  left: 0;
}

/* Member Cards */
.member-card {
  background: rgba(31, 41, 55, 0.6);
  backdrop-filter: blur(15px);
  border: 1px solid rgba(75, 85, 99, 0.3);
  border-radius: 1.5rem;
  overflow: hidden;
  transition: all 0.4s ease;
  position: relative;
}

.member-card:hover {
  transform: translateY(-5px);
  border-color: rgba(59, 130, 246, 0.5);
  box-shadow: 0 20px 40px rgba(59, 130, 246, 0.15);
}

.member-card-content {
  padding: 2rem;
  position: relative;
  z-index: 2;
}

.member-avatar {
  position: relative;
  margin: 0 auto 1.5rem;
  width: fit-content;
}

.avatar-placeholder {
  width: 80px;
  height: 80px;
  background: linear-gradient(135deg, #374151, #4b5563);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 2rem;
  color: #9ca3af;
  transition: all 0.3s ease;
}

.member-card:hover .avatar-placeholder {
  background: linear-gradient(135deg, #3b82f6, #8b5cf6);
  color: white;
  transform: scale(1.05);
}

.avatar-ring {
  position: absolute;
  top: -3px;
  left: -3px;
  right: -3px;
  bottom: -3px;
  border: 2px solid transparent;
  border-radius: 50%;
  background: linear-gradient(45deg, #3b82f6, #8b5cf6) border-box;
  mask: linear-gradient(#fff 0 0) padding-box, linear-gradient(#fff 0 0);
  mask-composite: exclude;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.member-card:hover .avatar-ring {
  opacity: 1;
}

.member-info {
  text-align: center;
}

.member-bg-decoration {
  position: absolute;
  top: -50%;
  right: -50%;
  width: 100%;
  height: 100%;
  background: radial-gradient(circle, rgba(59, 130, 246, 0.1) 0%, transparent 70%);
  transform: scale(0);
  transition: transform 0.4s ease;
  z-index: 1;
}

.member-card:hover .member-bg-decoration {
  transform: scale(1.5);
}

/* Avatar Image Styles */
.avatar-image-wrapper {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  overflow: hidden;
  position: relative;
  background: linear-gradient(135deg, #374151, #4b5563);
  transition: all 0.3s ease;
}

.avatar-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 50%;
  transition: all 0.3s ease;
}

.avatar-image:hover {
  transform: scale(1.1);
}

.avatar-placeholder {
  width: 80px;
  height: 80px;
  background: linear-gradient(135deg, #374151, #4b5563);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 2rem;
  color: #9ca3af;
  transition: all 0.3s ease;
}

.member-card:hover .avatar-image-wrapper {
  transform: scale(1.05);
}

.member-card:hover .avatar-placeholder {
  background: linear-gradient(135deg, #3b82f6, #8b5cf6);
  color: white;
  transform: scale(1.05);
}

/* Enhanced Avatar Ring */
.avatar-ring {
  position: absolute;
  top: -3px;
  left: -3px;
  right: -3px;
  bottom: -3px;
  border: 2px solid transparent;
  border-radius: 50%;
  background: linear-gradient(45deg, #3b82f6, #8b5cf6) border-box;
  mask: linear-gradient(#fff 0 0) padding-box, linear-gradient(#fff 0 0);
  mask-composite: exclude;
  -webkit-mask-composite: xor;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.member-card:hover .avatar-ring {
  opacity: 1;
  animation: ringRotate 2s linear infinite;
}

@keyframes ringRotate {
  from {
    transform: rotate(0deg);
  }

  to {
    transform: rotate(360deg);
  }
}

/* Image Loading States */
.avatar-image[data-loading="true"] {
  opacity: 0.5;
  background: linear-gradient(135deg, #374151, #4b5563);
}

.avatar-image-wrapper::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.1), transparent);
  transform: translateX(-100%);
  transition: transform 0.6s;
}

.member-card:hover .avatar-image-wrapper::before {
  transform: translateX(100%);
}

.social-btn {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  text-decoration: none;
  font-size: 1.1rem;
  transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  position: relative;
  overflow: hidden;
}

.social-btn::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  border-radius: 50%;
  transform: scale(0);
  transition: transform 0.3s ease;
  z-index: -1;
}

.social-btn:hover::before {
  transform: scale(1);
}

.instagram-btn {
  background: linear-gradient(45deg, #833ab4, #fd1d1d, #fcb045);
  border: 2px solid transparent;
}

.instagram-btn::before {
  background: linear-gradient(45deg, #a445b2, #fd1d1d, #fcb045);
}

.instagram-btn:hover {
  transform: translateY(-3px) scale(1.1);
  box-shadow: 0 10px 25px rgba(131, 58, 180, 0.4);
}

.email-btn {
  background: linear-gradient(45deg, #4285f4, #0f9d58);
  border: 2px solid transparent;
}

.email-btn::before {
  background: linear-gradient(45deg, #5a95f5, #0f9d58);
}

.email-btn:hover {
  transform: translateY(-3px) scale(1.1);
  box-shadow: 0 10px 25px rgba(66, 133, 244, 0.4);
}

.social-btn:active {
  transform: translateY(-1px) scale(1.05);
}

/* Enhanced Member Card for Social Links */
.member-card:hover .social-btn {
  transform: translateY(0);
}

.social-btn {
  opacity: 0.8;
  transition: all 0.3s ease;
}

.member-card:hover .social-btn {
  opacity: 1;
}

/* Tooltip effect */
.social-btn {
  position: relative;
}

.social-btn::after {
  content: attr(title);
  position: absolute;
  bottom: -35px;
  left: 50%;
  transform: translateX(-50%);
  background: rgba(0, 0, 0, 0.8);
  color: white;
  padding: 4px 8px;
  border-radius: 4px;
  font-size: 12px;
  white-space: nowrap;
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.3s ease;
  z-index: 1000;
}

.social-btn:hover::after {
  opacity: 1;
}

.close-btn {
  background: rgba(31, 41, 55, 0.8);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(75, 85, 99, 0.3);
  color: #e5e7eb;
  padding: 0.75rem 1.5rem;
  border-radius: 2rem;
  font-weight: 600;
  transition: all 0.3s ease;
  cursor: pointer;
}

.close-btn:hover {
  background: rgba(239, 68, 68, 0.2);
  border-color: rgba(239, 68, 68, 0.5);
  color: #fca5a5;
  transform: translateY(-2px);
}

/* Transitions */
.fade-slide-enter-active,
.fade-slide-leave-active {
  transition: all 0.5s ease;
}

.fade-slide-enter-from {
  opacity: 0;
  transform: translateY(20px);
}

.fade-slide-leave-to {
  opacity: 0;
  transform: translateY(-20px);
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

  .floating-orb {
    width: 100px !important;
    height: 100px !important;
  }

  .hero-glow {
    width: 300px;
    height: 300px;
  }

  .dept-card {
    min-height: 180px;
  }

  .dept-card-content {
    padding: 1.5rem;
  }

  .dept-icon {
    width: 50px;
    height: 50px;
    font-size: 1.25rem;
  }
}

@media (max-width: 640px) {
  .stats-card {
    padding: 1rem;
  }

  .stats-icon {
    width: 40px;
    height: 40px;
    font-size: 1rem;
  }

  .member-card-content {
    padding: 1.5rem;
  }

  .avatar-placeholder {
    width: 60px;
    height: 60px;
    font-size: 1.5rem;
  }
}

/* AOS Custom Animations */
[data-aos="zoom-in"] {
  opacity: 0;
  transform: scale(0.8);
  transition: opacity 0.6s ease, transform 0.6s ease;
}

[data-aos="zoom-in"].aos-animate {
  opacity: 1;
  transform: scale(1);
}

/* Loading Animation */
@keyframes shimmer {
  0% {
    background-position: -200px 0;
  }

  100% {
    background-position: calc(200px + 100%) 0;
  }
}

.loading-shimmer {
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.1), transparent);
  background-size: 200px 100%;
  animation: shimmer 1.5s infinite;
}
</style>