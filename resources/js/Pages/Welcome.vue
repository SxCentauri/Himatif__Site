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
  
<section id="about" class="relative py-28 bg-gradient-to-b from-gray-900 to-gray-950 overflow-hidden">
      <div class="container mx-auto px-6 md:px-12 text-center relative z-10">
        <!-- Badge -->
        <span class="enhanced-badge px-6 py-3 rounded-full text-sm text-blue-400 border border-blue-500/30 bg-blue-500/10" data-aos="fade-down">
          About HIMATIF
        </span>

        <!-- Title -->
        <h2 class="section-title text-4xl md:text-5xl font-bold text-white mt-6 mb-8" data-aos="fade-up">
          About HIMATIF
        </h2>

        <!-- Desc -->
        <p class="text-gray-300 max-w-3xl mx-auto leading-relaxed mb-16 text-lg" data-aos="fade-up" data-aos-delay="200">
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
              Menjadi wadah pengembangan potensi mahasiswa Teknik Informatika yang berkualitas, inovatif, dan berdaya saing global melalui kegiatan akademik dan non-akademik yang terstruktur dan berkelanjutan.
            </p>
          </div>
          <div class="mission-vision-card" data-aos="fade-left">
            <h3 class="text-2xl font-bold text-blue-400 mb-4">Our Vision</h3>
            <p class="text-gray-300 text-lg">
              Membangun generasi teknologi yang unggul, berkarakter, dan berkontribusi positif bagi perkembangan teknologi informasi di Indonesia melalui berbagai program dan kegiatan yang bermanfaat.
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
    <h2 class="section-title text-3xl md:text-4xl font-bold text-white mt-4 mb-4"
        data-aos="fade-up"
        data-aos-delay="100">
      What They Say
    </h2>
    <p class="text-gray-400 max-w-2xl mx-auto mb-12"
       data-aos="fade-up"
       data-aos-delay="200">
      Dengarkan pengalaman dan cerita dari para alumni HIMATIF UNIB yang telah sukses dalam karir mereka.
    </p>

    <!-- Swiper -->
    <div class="swiper mySwiper" data-aos="zoom-in" data-aos-delay="300">
      <div class="swiper-wrapper">
        <!-- Testimoni 1 -->
        <div class="swiper-slide ">
          <div class="testimonial-card mt-8 bg-gray-800/80 p-8 rounded-2xl shadow-lg h-full flex flex-col justify-between min-h-[480px] max-w-[320px] mx-auto z-0 backdrop-blur-sm border border-gray-700/50">
            <div class="quote-icon mb-4">
              <svg class="w-8 h-8 text-blue-400 mx-auto" fill="currentColor" viewBox="0 0 24 24">
                <path d="M14.017 21v-7.391c0-5.704 3.731-9.57 8.983-10.609l.995 2.151c-2.432.917-3.995 3.638-3.995 5.849h4v10h-10zm-14.017 0v-7.391c0-5.704 3.748-9.57 9-10.609l.996 2.151c-2.433.917-3.996 3.638-3.996 5.849h4v10h-10z"/>
              </svg>
            </div>
            <p class="quote-text text-gray-300 italic mb-8 text-lg leading-relaxed">
              "Bergabung dengan HIMATIF UNIB memberikan saya lebih dari sekadar pengalaman berorganisasi. 
              Di sini saya menemukan keluarga, tempat karakter dibentuk, dan peluang besar untuk berkembang."
            </p>
            <div class="profile-section flex items-center gap-4 mt-auto">
              <div class="profile-img-container">
                <img src="./img/profile1.png" 
                     alt="Naufal Nazhif A." 
                     class="profile-img w-16 h-16 rounded-full border-2 border-blue-400 object-cover" />
                <div class="absolute inset-0 rounded-full bg-blue-400/20 opacity-0 transition-opacity duration-300"></div>
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
          <div class="testimonial-card mt-8 bg-gray-800/80 p-8 rounded-2xl shadow-lg h-full flex flex-col justify-between min-h-[480px] max-w-[320px] mx-auto z-0 backdrop-blur-sm border border-gray-700/50">
            <div class="quote-icon mb-4">
              <svg class="w-8 h-8 text-blue-400 mx-auto" fill="currentColor" viewBox="0 0 24 24">
                <path d="M14.017 21v-7.391c0-5.704 3.731-9.57 8.983-10.609l.995 2.151c-2.432.917-3.995 3.638-3.995 5.849h4v10h-10zm-14.017 0v-7.391c0-5.704 3.748-9.57 9-10.609l.996 2.151c-2.433.917-3.996 3.638-3.996 5.849h4v10h-10z"/>
              </svg>
            </div>
            <p class="quote-text text-gray-300 italic mb-8 text-lg leading-relaxed">
              "Menjadi bagian dari HIMATIF UNIB adalah salah satu pengalaman paling berkesan. 
              Saya belajar kepemimpinan, manajemen, dan membangun relasi yang luas."
            </p>
            <div class="profile-section flex items-center gap-4 mt-auto">
              <div class="profile-img-container relative">
                <img src="./img/profile1.png" 
                     alt="M Dzawil Fadhol A." 
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
          <div class="testimonial-card mt-8 bg-gray-800/80 p-8 rounded-2xl shadow-lg h-full flex flex-col justify-between min-h-[480px] max-w-[320px] mx-auto z-0 backdrop-blur-sm border border-gray-700/50">
            <div class="quote-icon mb-4">
              <svg class="w-8 h-8 text-blue-400 mx-auto" fill="currentColor" viewBox="0 0 24 24">
                <path d="M14.017 21v-7.391c0-5.704 3.731-9.57 8.983-10.609l.995 2.151c-2.432.917-3.995 3.638-3.995 5.849h4v10h-10zm-14.017 0v-7.391c0-5.704 3.748-9.57 9-10.609l.996 2.151c-2.433.917-3.996 3.638-3.996 5.849h4v10h-10z"/>
              </svg>
            </div>
            <p class="quote-text text-gray-300 italic mb-8 text-lg leading-relaxed">
              "Merupakan keputusan tepat bergabung dengan HIMATIF. Saya mendapatkan pengalaman baru, 
              relasi luas, dan kesempatan untuk mengasah keterampilan."
            </p>
            <div class="profile-section flex items-center gap-4 mt-auto">
              <div class="profile-img-container relative">
                <img src="./img/profile1.png" 
                     alt="Vellanindhita" 
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
          <div class="testimonial-card mt-8 bg-gray-800/80 p-8 rounded-2xl shadow-lg h-full flex flex-col justify-between min-h-[480px] max-w-[320px] mx-auto z-0 backdrop-blur-sm border border-gray-700/50">
            <div class="quote-icon mb-4">
              <svg class="w-8 h-8 text-blue-400 mx-auto" fill="currentColor" viewBox="0 0 24 24">
                <path d="M14.017 21v-7.391c0-5.704 3.731-9.57 8.983-10.609l.995 2.151c-2.432.917-3.995 3.638-3.995 5.849h4v10h-10zm-14.017 0v-7.391c0-5.704 3.748-9.57 9-10.609l.996 2.151c-2.433.917-3.996 3.638-3.996 5.849h4v10h-10z"/>
              </svg>
            </div>
            <p class="quote-text text-gray-300 italic mb-8 text-lg leading-relaxed">
              "HIMATIF telah memberikan saya platform untuk mengembangkan diri dan berkontribusi pada komunitas. 
              Pengalaman yang tak terlupakan dengan teman-teman hebat."
            </p>
            <div class="profile-section flex items-center gap-4 mt-auto">
              <div class="profile-img-container relative">
                <img src="./img/profile1.png" 
                     alt="Alumni" 
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
          <div class="testimonial-card mt-8 bg-gray-800/80 p-8 rounded-2xl shadow-lg h-full flex flex-col justify-between min-h-[480px] max-w-[320px] mx-auto z-0 backdrop-blur-sm border border-gray-700/50">
            <div class="quote-icon mb-4">
              <svg class="w-8 h-8 text-blue-400 mx-auto" fill="currentColor" viewBox="0 0 24 24">
                <path d="M14.017 21v-7.391c0-5.704 3.731-9.57 8.983-10.609l.995 2.151c-2.432.917-3.995 3.638-3.995 5.849h4v10h-10zm-14.017 0v-7.391c0-5.704 3.748-9.57 9-10.609l.996 2.151c-2.433.917-3.996 3.638-3.996 5.849h4v10h-10z"/>
              </svg>
            </div>
            <p class="quote-text text-gray-300 italic mb-8 text-lg leading-relaxed">
              "Organisasi ini mengajarkan saya tentang teamwork, leadership, dan problem solving. 
              Skills yang sangat berharga untuk karir di bidang teknologi."
            </p>
            <div class="profile-section flex items-center gap-4 mt-auto">
              <div class="profile-img-container relative">
                <img src="./img/profile1.png" 
                     alt="Alumni" 
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
    <span class="enhanced-badge px-6 py-3 rounded-full text-sm text-blue-400 border border-blue-500/30 bg-blue-500/10 block w-fit mx-auto" data-aos="fade-down">
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
        <div class="faq-item rounded-xl transition-all duration-300 ease-out" 
             data-aos="fade-up" 
             data-aos-delay="300">
          <button class="faq-header w-full flex items-center justify-between p-6 text-left rounded-xl transition-all duration-300">
            <div class="flex items-center space-x-4">
              <div class="faq-icon w-8 h-8 rounded-full bg-blue-500/20 flex items-center justify-center">
                <svg class="w-4 h-4 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8.228 9c.549-1.165 2.03-2 3.772-2 2.21 0 4 1.343 4 3 0 1.4-1.278 2.575-3.006 2.907-.542.104-.994.54-.994 1.093m0 3h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"/>
                </svg>
              </div>
              <h3 class="font-semibold text-lg text-white">Apa itu HIMATIF?</h3>
            </div>
            <div class="faq-chevron transition-transform duration-300">
              <svg class="w-5 h-5 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"/>
              </svg>
            </div>
          </button>
          <div class="faq-content overflow-hidden transition-all duration-500 ease-out max-h-0 opacity-0">
            <div class="px-6 pb-6">
              <div class="pl-12">
                <p class="text-gray-300 leading-relaxed">
                  Himpunan Mahasiswa Teknik Informatika (HIMATIF) adalah organisasi kemahasiswaan tingkat jurusan yang menaungi seluruh mahasiswa Program Studi Teknik Informatika. HIMATIF berfungsi sebagai wadah untuk mengembangkan potensi akademik dan non-akademik mahasiswa serta menjembatani komunikasi antara mahasiswa, dosen, dan pihak eksternal.
                </p>
              </div>
            </div>
          </div>
        </div>

        <!-- FAQ Item 2 -->
        <div class="faq-item rounded-xl transition-all duration-300 ease-out" 
             data-aos="fade-up" 
             data-aos-delay="350">
          <button class="faq-header w-full flex items-center justify-between p-6 text-left rounded-xl transition-all duration-300">
            <div class="flex items-center space-x-4">
              <div class="faq-icon w-8 h-8 rounded-full bg-blue-500/20 flex items-center justify-center">
                <svg class="w-4 h-4 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 11H5m14-5v12a2 2 0 01-2 2H7a2 2 0 01-2-2V6a2 2 0 012-2h10a2 2 0 012 2z"/>
                </svg>
              </div>
              <h3 class="font-semibold text-lg text-white">Apa saja Program HIMATIF?</h3>
            </div>
            <div class="faq-chevron transition-transform duration-300">
              <svg class="w-5 h-5 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"/>
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
        <div class="faq-item rounded-xl transition-all duration-300 ease-out" 
             data-aos="fade-up" 
             data-aos-delay="400">
          <button class="faq-header w-full flex items-center justify-between p-6 text-left rounded-xl transition-all duration-300">
            <div class="flex items-center space-x-4">
              <div class="faq-icon w-8 h-8 rounded-full bg-blue-500/20 flex items-center justify-center">
                <svg class="w-4 h-4 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197m13.5-9a2.5 2.5 0 11-5 0 2.5 2.5 0 015 0z"/>
                </svg>
              </div>
              <h3 class="font-semibold text-lg text-white">Bagaimana cara bergabung dengan HIMATIF?</h3>
            </div>
            <div class="faq-chevron transition-transform duration-300">
              <svg class="w-5 h-5 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"/>
              </svg>
            </div>
          </button>
          <div class="faq-content overflow-hidden transition-all duration-500 ease-out max-h-0 opacity-0">
            <div class="px-6 pb-6">
              <div class="pl-12">
                <p class="text-gray-300 leading-relaxed">
                  Setiap mahasiswa aktif Program Studi Teknik Informatika secara otomatis menjadi anggota HIMATIF. Untuk terlibat aktif dalam kegiatan organisasi, Anda dapat mengikuti rekrutmen pengurus yang biasanya diadakan setiap tahun atau bergabung dalam berbagai kepanitiaan event yang diselenggarakan HIMATIF.
                </p>
              </div>
            </div>
          </div>
        </div>

        <!-- FAQ Item 4 -->
        <div class="faq-item rounded-xl transition-all duration-300 ease-out" 
             data-aos="fade-up" 
             data-aos-delay="450">
          <button class="faq-header w-full flex items-center justify-between p-6 text-left rounded-xl transition-all duration-300">
            <div class="flex items-center space-x-4">
              <div class="faq-icon w-8 h-8 rounded-full bg-blue-500/20 flex items-center justify-center">
                <svg class="w-4 h-4 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9.663 17h4.673M12 3v1m6.364 1.636l-.707.707M21 12h-1M4 12H3m3.343-5.657l-.707-.707m2.828 9.9a5 5 0 117.072 0l-.548.547A3.374 3.374 0 0014 18.469V19a2 2 0 11-4 0v-.531c0-.895-.356-1.754-.988-2.386l-.548-.547z"/>
                </svg>
              </div>
              <h3 class="font-semibold text-lg text-white">Apa manfaat bergabung dengan HIMATIF?</h3>
            </div>
            <div class="faq-chevron transition-transform duration-300">
              <svg class="w-5 h-5 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"/>
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
        <div class="faq-item rounded-xl transition-all duration-300 ease-out" 
             data-aos="fade-up" 
             data-aos-delay="500">
          <button class="faq-header w-full flex items-center justify-between p-6 text-left rounded-xl transition-all duration-300">
            <div class="flex items-center space-x-4">
              <div class="faq-icon w-8 h-8 rounded-full bg-blue-500/20 flex items-center justify-center">
                <svg class="w-4 h-4 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"/>
                </svg>
              </div>
              <h3 class="font-semibold text-lg text-white">Berapa lama masa kepengurusan HIMATIF?</h3>
            </div>
            <div class="faq-chevron transition-transform duration-300">
              <svg class="w-5 h-5 text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"/>
              </svg>
            </div>
          </button>
          <div class="faq-content overflow-hidden transition-all duration-500 ease-out max-h-0 opacity-0">
            <div class="px-6 pb-6">
              <div class="pl-12">
                <p class="text-gray-300 leading-relaxed">
                  Masa kepengurusan HIMATIF berlangsung selama satu tahun akademik. Periode kepengurusan dimulai dari pelantikan pengurus baru hingga pelantikan pengurus periode berikutnya. Selama masa ini, pengurus akan menjalankan program kerja yang telah direncanakan serta mengkoordinasikan berbagai kegiatan untuk kemajuan organisasi dan anggota.
                </p>
              </div>
            </div>
          </div>
        </div>
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
  name: "Testimonials",
  mounted() {
    // ✅ Inisialisasi AOS
    import("aos").then((AOS) => {
      AOS.init({
        duration: 1000,
        once: true,
        easing: "ease-out-quart",
      });
    });

    // ✅ Inisialisasi Swiper
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

    // ✅ Fungsi FAQ Accordion
    const faqHeaders = document.querySelectorAll(".faq-header");

    faqHeaders.forEach((header) => {
      header.addEventListener("click", function () {
        const faqItem = this.parentElement;
        const content = this.nextElementSibling;
        const chevron = this.querySelector(".faq-chevron");

        // Tutup semua FAQ items lainnya
        document.querySelectorAll(".faq-item").forEach((item) => {
          if (item !== faqItem) {
            item.classList.remove("active");
            item.querySelector(".faq-content").classList.remove("max-h-96", "opacity-100");
            item.querySelector(".faq-content").classList.add("max-h-0", "opacity-0");
            item.querySelector(".faq-chevron").classList.remove("rotate-180");
          }
        });

        // Toggle FAQ item yang diklik
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
  },
};
</script>
  
<style>
/* CSS yang Anda berikan */
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
    0%, 100% { transform: translateY(0px) translateX(0px) rotate(0deg) scale(1); }
    25% { transform: translateY(-30px) translateX(20px) rotate(90deg) scale(1.1); }
    50% { transform: translateY(-15px) translateX(-15px) rotate(180deg) scale(0.9); }
    75% { transform: translateY(-40px) translateX(10px) rotate(270deg) scale(1.05); }
}

@keyframes float2 {
    0%, 100% { transform: translateY(0px) translateX(0px) rotate(0deg) scale(1); }
    33% { transform: translateY(-25px) translateX(-25px) rotate(120deg) scale(1.08); }
    66% { transform: translateY(-35px) translateX(15px) rotate(240deg) scale(0.95); }
}

@keyframes float3 {
    0%, 100% { transform: translateY(0px) translateX(0px) rotate(0deg) scale(1); }
    20% { transform: translateY(-20px) translateX(-10px) rotate(72deg) scale(1.12); }
    40% { transform: translateY(-35px) translateX(20px) rotate(144deg) scale(0.88); }
    60% { transform: translateY(-25px) translateX(-20px) rotate(216deg) scale(1.06); }
    80% { transform: translateY(-40px) translateX(10px) rotate(288deg) scale(0.92); }
}

@keyframes enhanced-pulse {
    0%, 100% { opacity: 0.15; transform: scale(1); }
    50% { opacity: 0.25; transform: scale(1.05); }
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
</style>