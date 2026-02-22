<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const slides = [
  {
    id: 1,
    name: 'BALLET',
    description: 'Discover the grace, precision, and timeless elegance of classical ballet.',
    image: 'http://static.wixstatic.com/media/61bce3_d3ba111ff4e044159bebf9a984a399c2~mv2.jpg/v1/fit/w_781,h_763,q_90,enc_avif,quality_auto/61bce3_d3ba111ff4e044159bebf9a984a399c2~mv2.jpg',
    color: 'from-purple-500/10'
  },
  {
    id: 2,
    name: 'HUSTLERS',
    description: 'Feel the rhythm and master the energy of urban street dance styles.',
    image: 'https://static.wixstatic.com/media/61bce3_735f6fde06194207a775ebd237a80a4c~mv2.png/v1/fit/w_781,h_763,q_90,enc_avif,quality_auto/61bce3_735f6fde06194207a775ebd237a80a4c~mv2.png',
    color: 'from-[#ff2e96]/10'
  },
  {
    id: 3,
    name: 'INTENSIVE',
    description: 'Specialized programs designed to fast-track your journey to professional dancing.',
    image: 'https://static.wixstatic.com/media/61bce3_2cddf9ce48fd4fee8ab40a5141b6d0dd~mv2.jpg/v1/fit/w_781,h_763,q_90,enc_avif,quality_auto/61bce3_2cddf9ce48fd4fee8ab40a5141b6d0dd~mv2.jpg',
    color: 'from-blue-500/10'
  },
  {
    id: 4,
    name: 'BACHATA',
    description: 'Feel the passion and smooth rhythms of this sensual Latin dance style.',
    image: 'https://static.wixstatic.com/media/61bce3_09827acdeb554d24b5db0c1dbaf54bd4~mv2.jpg/v1/fit/w_781,h_763,q_90,enc_avif,quality_auto/61bce3_09827acdeb554d24b5db0c1dbaf54bd4~mv2.jpg',
    color: 'from-orange-500/10'
  }
]

const gallery = [
  { id: 1, image: 'https://static.wixstatic.com/media/61bce3_e9bd7e7123b547be882f23b9177f98b8~mv2.jpg/v1/fit/w_781,h_763,q_90,enc_avif,quality_auto/61bce3_e9bd7e7123b547be882f23b9177f98b8~mv2.jpg', title: 'BALLET' },
  { id: 2, image: 'https://static.wixstatic.com/media/61bce3_09827acdeb554d24b5db0c1dbaf54bd4~mv2.jpg/v1/fit/w_781,h_763,q_90,enc_avif,quality_auto/61bce3_09827acdeb554d24b5db0c1dbaf54bd4~mv2.jpg', title: 'BACHATA' },
  { id: 3, image: 'https://static.wixstatic.com/media/61bce3_2cddf9ce48fd4fee8ab40a5141b6d0dd~mv2.jpg/v1/fit/w_781,h_763,q_90,enc_avif,quality_auto/61bce3_2cddf9ce48fd4fee8ab40a5141b6d0dd~mv2.jpg', title: 'INTENSIVE' },
  { id: 4, image: 'http://static.wixstatic.com/media/61bce3_d3ba111ff4e044159bebf9a984a399c2~mv2.jpg/v1/fit/w_781,h_763,q_90,enc_avif,quality_auto/61bce3_d3ba111ff4e044159bebf9a984a399c2~mv2.jpg', title: 'BALLET' },
  { id: 5, image: 'https://static.wixstatic.com/media/61bce3_b360cbf7874a40fa8eb0aa5163aa92e4~mv2.jpg/v1/fit/w_781,h_763,q_90,enc_avif,quality_auto/61bce3_b360cbf7874a40fa8eb0aa5163aa92e4~mv2.jpg', title: 'GYMNASTICS' },
  { id: 6, image: 'https://static.wixstatic.com/media/61bce3_35dfd2f1c25a4789811f9a7b9cfc1d69~mv2.jpg/v1/fit/w_781,h_763,q_90,enc_avif,quality_auto/61bce3_35dfd2f1c25a4789811f9a7b9cfc1d69~mv2.jpg', title: 'HIP HOP' },
  { id: 7, image: 'https://static.wixstatic.com/media/61bce3_735f6fde06194207a775ebd237a80a4c~mv2.png/v1/fit/w_781,h_763,q_90,enc_avif,quality_auto/61bce3_735f6fde06194207a775ebd237a80a4c~mv2.png', title: 'HUSTLERS' },
]

const reviews = [
  {
    id: 1,
    name: 'Sarah M.',
    text: 'Fun, well-organized classes with professional instructors. Perfect for beginners, providing a motivating atmosphere that makes you look forward to every session.',
    rating: 5,
    role: 'Student'
  },
  {
    id: 2,
    name: 'Ahmed K.',
    text: 'Welcoming and energetic atmosphere! Passionate instructors provide clear guidance and encouragement. I always leave class feeling more confident and happy.',
    rating: 5,
    role: 'Student'
  },
  {
    id: 3,
    name: 'Laila R.',
    text: 'Amazing vibe and supportive community! Instructors make learning simple and fun, even for beginners. Gained confidence and made new friends along the way.',
    rating: 5,
    role: 'Student'
  }
]

const currentIndex = ref(0)
const isAutoPlaying = ref(true)
let autoPlayInterval = null

const nextSlide = () => {
  currentIndex.value = (currentIndex.value + 1) % slides.length
}

const prevSlide = () => {
  currentIndex.value = (currentIndex.value - 1 + slides.length) % slides.length
}

const goToSlide = (index) => {
  currentIndex.value = index
}

const startAutoPlay = () => {
  autoPlayInterval = setInterval(nextSlide, 5000)
}

const stopAutoPlay = () => {
  if (autoPlayInterval) clearInterval(autoPlayInterval)
}

const isMenuOpen = ref(false)
const activeSection = ref('home')
const scrolled = ref(false)

const navLinks = [
  { name: 'Home', id: 'home' },
  { name: 'About', id: 'about' },
  { name: 'Gallery', id: 'gallery' },
  { name: 'Reviews', id: 'reviews' },
  { name: 'Contact', id: 'contact' }
]

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value
  if (isMenuOpen.value) {
    document.body.style.overflow = 'hidden'
  } else {
    document.body.style.overflow = ''
  }
}

const handleScroll = () => {
  scrolled.value = window.scrollY > 50

  // Active section tracking
  const sections = navLinks.map(link => document.getElementById(link.id))
  const scrollPosition = window.scrollY + 100

  sections.forEach(section => {
    if (section) {
      const top = section.offsetTop
      const height = section.offsetHeight
      if (scrollPosition >= top && scrollPosition < top + height) {
        activeSection.value = section.id
      }
    }
  })
}

const scrollToTop = () => {
  window.scrollTo({
    top: 0,
    behavior: 'smooth'
  })
}

onMounted(() => {
  startAutoPlay()
  window.addEventListener('scroll', handleScroll)

  // Reveal animations
  const observerOptions = {
    threshold: 0.1
  }

  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('reveal-visible')
      }
    })
  }, observerOptions)

  document.querySelectorAll('.reveal').forEach(el => observer.observe(el))
})

onUnmounted(() => {
  stopAutoPlay()
  window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
  <div class="min-h-screen bg-[#fafafc] font-['Outfit'] relative overflow-hidden flex flex-col scroll-smooth">
    <!-- Background accents -->
    <div
      class="fixed top-[-10%] left-[-10%] w-[40%] h-[40%] rounded-full blur-[120px] transition-all duration-1000 opacity-60 z-0 pointer-events-none"
      :class="slides[currentIndex].color.replace('from-', 'bg-')"></div>
    <div
      class="fixed bottom-[-10%] right-[-10%] w-[40%] h-[40%] bg-purple-500/5 rounded-full blur-[120px] z-0 pointer-events-none">
    </div>

    <!-- Header / Navbar -->
    <header :class="[
      'fixed top-0 left-0 right-0 z-[100] transition-all duration-500 md:px-6 lg:px-8',
      scrolled ? 'py-4' : 'py-8'
    ]">
      <nav :class="[
        'max-w-7xl mx-auto flex items-center justify-between px-6 py-4 transition-all duration-500 border relative overflow-hidden',
        scrolled ? 'bg-white/80 backdrop-blur-2xl border-black/5 shadow-lg rounded-full' : 'bg-white/40 backdrop-blur-xl border-white/20 rounded-3xl'
      ]">
        <!-- Glass highlight -->
        <div v-if="!scrolled" class="absolute inset-0 bg-gradient-to-tr from-white/20 to-transparent opacity-50"></div>

        <!-- Logo -->
        <a href="#home" class="flex items-center gap-3 relative z-10 group">
          <!-- <div class="h-10 w-10 flex items-center justify-center relative"> -->
          <!-- <div class="absolute inset-0 bg-[#ff2e96]/20 rounded-xl blur-lg group-hover:blur-xl transition-all"></div> -->
          <!-- <div
              class="relative w-full h-full bg-gradient-to-tr from-[#ff2e96] to-[#9240f4] rounded-xl flex items-center justify-center p-2 shadow-lg shadow-pink-500/20">
              <svg viewBox="0 0 24 24" fill="none" class="w-full h-full stroke-white stroke-[2.5]"
                stroke-linecap="round" stroke-linejoin="round">
                <path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5" />
              </svg>
            </div> -->
          <!-- </div> -->
          <span class="text-gray-900 font-bold text-lg tracking-tight uppercase">ADAM'S <span
              class="text-[#ff2e96] font-black">DANCE</span></span>
        </a>

        <!-- Desktop Links -->
        <div class="hidden md:flex items-center gap-1 relative z-10">
          <a v-for="link in navLinks" :key="link.id" :href="'#' + link.id" :class="[
            'px-5 py-2 rounded-full text-xs uppercase tracking-[0.2em] font-bold transition-all duration-300 relative group overflow-hidden',
            activeSection === link.id ? 'text-[#ff2e96] bg-[#ff2e96]/5' : 'text-gray-500 hover:text-gray-900 hover:bg-black/5'
          ]">
            {{ link.name }}
          </a>
        </div>

        <!-- Desktop CTA -->
        <div class="hidden md:flex items-center gap-4 relative z-10">
          <button
            class="bg-gradient-to-r from-[#ff2e96] to-[#9240f4] text-white px-7 py-3 rounded-full font-bold text-xs transition-all duration-300 hover:scale-105 hover:shadow-[0_8px_25px_rgba(255,46,150,0.4)] active:scale-95 uppercase tracking-widest">
            Book Class
          </button>
        </div>

        <!-- Mobile Menu Toggle -->
        <button @click="toggleMenu" class="md:hidden relative z-10 p-2 text-gray-900">
          <svg v-if="!isMenuOpen" xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24"
            stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16m-7 6h7" />
          </svg>
          <svg v-else xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24"
            stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
          </svg>
        </button>
      </nav>

      <!-- Mobile Menu Overlay -->
      <Transition name="fade">
        <div v-if="isMenuOpen" class="fixed inset-0 z-[90] bg-white md:hidden overflow-y-auto pt-32 px-8 pb-12">
          <div class="space-y-8">
            <a v-for="(link, i) in navLinks" :key="link.id" :href="'#' + link.id" @click="toggleMenu"
              class="block text-4xl font-black text-gray-900 hover:text-[#ff2e96] transition-colors"
              :style="{ animationDelay: (i * 100) + 'ms' }">
              {{ link.name }}.
            </a>
            <div class="pt-12">
              <button
                class="w-full bg-[#ff2e96] text-white py-5 rounded-3xl font-black text-lg shadow-xl shadow-pink-500/20">
                JOIN THE STUDIO
              </button>
            </div>
          </div>
        </div>
      </Transition>
    </header>

    <!-- Main Content / Carousel -->
    <main id="home" class="flex-grow relative flex items-center z-10 py-32 md:py-48 mt-10">
      <div class="max-w-7xl mx-auto w-full px-4 sm:px-6 lg:px-8 grid grid-cols-1 lg:grid-cols-2 gap-20 items-center">

        <!-- Text Content -->
        <div class="space-y-10 order-2 lg:order-1 reveal">
          <div class="inline-block px-5 py-2 bg-black/5 border border-black/5 rounded-full backdrop-blur-sm">
            <span class="text-[#ff2e96] text-xs font-black uppercase tracking-[0.4em]">The Elite Studio</span>
          </div>

          <div class="relative overflow-hidden h-[130px]">
            <TransitionGroup name="slide-up">
              <h1 v-for="(slide, index) in slides" v-show="index === currentIndex" :key="slide.id"
                class="text-6xl sm:text-8xl font-black text-gray-900 absolute inset-0 leading-none">
                {{ slide.name }}<span class="text-[#ff2e96]">.</span>
              </h1>
            </TransitionGroup>
          </div>

          <p class="text-gray-500 text-xl sm:text-2xl max-w-lg leading-relaxed font-medium">
            {{ slides[currentIndex].description }}
          </p>

          <div class="flex flex-wrap items-center gap-6">
            <button
              class="px-10 py-5 bg-gray-900 text-white font-black rounded-3xl hover:bg-[#ff2e96] transition-all duration-500 flex items-center gap-4 group shadow-2xl shadow-black/10">
              EXPLORE CLASSES
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 group-hover:translate-x-2 transition-transform"
                fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 8l4 4m0 0l-4 4m4-4H3" />
              </svg>
            </button>
            <div class="flex -space-x-3">
              <img v-for="i in 3" :key="i" :src="'https://i.pravatar.cc/100?img=' + (i + 10)"
                class="w-12 h-12 rounded-full border-4 border-white object-cover" loading="lazy">
              <div
                class="w-12 h-12 rounded-full border-4 border-white bg-gray-100 flex items-center justify-center text-[10px] font-black text-gray-400 leading-none">
                500+</div>
            </div>
            <div class="text-xs uppercase tracking-widest font-black text-gray-400">Join our community</div>
          </div>

          <!-- Controls -->
          <div class="flex items-center gap-6 pt-12">
            <button @click="prevSlide"
              class="w-14 h-14 rounded-full border border-black/10 flex items-center justify-center text-gray-900 hover:bg-[#ff2e96] hover:text-white hover:border-[#ff2e96] transition-all group">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 group-hover:-translate-x-1 transition-transform"
                fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
              </svg>
            </button>
            <div class="flex items-center gap-3">
              <button v-for="(_, index) in slides" :key="index" @click="goToSlide(index)"
                class="h-2 transition-all duration-500 rounded-full"
                :class="index === currentIndex ? 'w-12 bg-[#ff2e96]' : 'w-3 bg-black/10 hover:bg-black/20'"></button>
            </div>
            <button @click="nextSlide"
              class="w-14 h-14 rounded-full border border-black/10 flex items-center justify-center text-gray-900 hover:bg-[#ff2e96] hover:text-white hover:border-[#ff2e96] transition-all group">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 group-hover:translate-x-1 transition-transform"
                fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
              </svg>
            </button>
          </div>
        </div>

        <!-- Image Content -->
        <div class="relative flex justify-center order-1 lg:order-2 reveal">
          <div class="relative w-full max-w-lg aspect-[4/5] sm:aspect-[4/5] scale-105">
            <!-- Decorative accents -->
            <div class="absolute -top-12 -right-12 w-64 h-64 bg-pink-500/10 rounded-full blur-[80px]"></div>
            <div class="absolute -bottom-12 -left-12 w-64 h-64 bg-purple-500/10 rounded-full blur-[80px]"></div>

            <!-- Image Frame -->
            <div
              class="w-full h-full rounded-[4rem] overflow-hidden border-8 border-white/50 shadow-[0_32px_120px_-20px_rgba(0,0,0,0.25)] relative group">
              <Transition name="fade">
                <img :key="currentIndex" :src="slides[currentIndex].image"
                  class="w-full h-full object-cover transition-transform duration-1000 group-hover:scale-105"
                  alt="Dance Movement" decoding="async">
              </Transition>
              <div class="absolute inset-0 bg-gradient-to-t from-black/40 via-transparent to-transparent opacity-60">
              </div>

              <!-- Floating Badge -->
              <div
                class="absolute bottom-10 left-10 right-10 p-6 bg-white/20 backdrop-blur-2xl border border-white/30 rounded-3xl shadow-2xl">
                <div class="flex items-center gap-4">
                  <div
                    class="w-12 h-12 rounded-xl bg-[#ff2e96] flex items-center justify-center text-white font-black text-lg">
                    0{{ currentIndex + 1 }}</div>
                  <div>
                    <div class="text-white font-black text-sm uppercase tracking-widest">{{ slides[currentIndex].name }}
                    </div>
                    <div class="text-white/70 text-[10px] uppercase font-bold tracking-[0.2em] pt-1">Advanced Training
                      Available</div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

      </div>
    </main>

    <!-- About Section -->
    <section id="about" class="py-24 bg-white relative z-10">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-16 items-center">

          <!-- About Image Side -->
          <div class="relative order-2 lg:order-1">
            <div class="relative rounded-[3rem] overflow-hidden shadow-2xl aspect-[4/5]">
              <img src="https://images.unsplash.com/photo-1518834107812-67b0b7c58434?q=80&w=1935&auto=format&fit=crop"
                alt="Studio Interior" class="w-full h-full object-cover">
              <div class="absolute inset-0 bg-gradient-to-tr from-[#ff2e96]/20 to-transparent"></div>
            </div>
            <!-- Stats Badge -->
            <div
              class="absolute -bottom-10 -right-10 bg-white p-8 rounded-[2rem] shadow-xl border border-black/5 hidden md:block">
              <div class="flex items-center gap-4">
                <div class="text-5xl font-black text-[#ff2e96]">6+</div>
                <div class="text-sm font-bold text-gray-900 leading-tight uppercase tracking-wider">
                  Years of<br>Excellence
                </div>
              </div>
            </div>
          </div>

          <!-- About Text Side -->
          <div class="space-y-8 order-1 lg:order-2">
            <div class="inline-block px-4 py-1.5 bg-[#ff2e96]/5 border border-[#ff2e96]/10 rounded-full">
              <span class="text-[#ff2e96] text-xs font-bold uppercase tracking-[0.3em]">Our Story</span>
            </div>

            <h2 class="text-4xl sm:text-5xl font-black text-gray-900 leading-tight">
              About Adams <br><span class="text-[#ff2e96]">Dance Studio.</span>
            </h2>

            <div class="space-y-6 text-gray-600 text-lg leading-relaxed">
              <p>
                Founded from the heart of Cairo, Adams Dance Studio incorporates many genres including
                <span class="text-gray-900 font-semibold">Hip Hop, Contemporary, Salsa</span> and much more.
                With a handful of professional instructors, we provide dance classes from beginner to advanced levels.
              </p>

              <p>
                The dance studio is like no other as it also caters intensive programs to become a professional
                dancer and also private and wedding packages. Adams have been operating for 6 years now and
                has three branches in <span class="text-[#ff2e96] font-bold">New Cairo, Katameya, and Sheikh
                  Zayed</span>.
              </p>

              <p class="font-medium text-gray-800">
                Are you ready to get up and move? Contact us today to learn more about our studio.
              </p>
            </div>

            <!-- Features Grid -->
            <div class="grid grid-cols-2 gap-6 pt-8">
              <div class="flex items-start gap-4">
                <div
                  class="w-12 h-12 rounded-xl bg-purple-50 flex items-center justify-center text-purple-600 shrink-0">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24"
                    stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                      d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" />
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                      d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
                  </svg>
                </div>
                <div>
                  <h4 class="font-bold text-gray-900">3 Branches</h4>
                  <p class="text-sm text-gray-500">Cairo's top locations</p>
                </div>
              </div>
              <div class="flex items-start gap-4">
                <div class="w-12 h-12 rounded-xl bg-pink-50 flex items-center justify-center text-[#ff2e96] shrink-0">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24"
                    stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                      d="M12 4.354a4 4 0 110 5.292M15 21H3v-1a6 6 0 0112 0v1zm0 0h6v-1a6 6 0 00-9-5.197M13 7a4 4 0 11-8 0 4 4 0 018 0z" />
                  </svg>
                </div>
                <div>
                  <h4 class="font-bold text-gray-900">Pro Coaches</h4>
                  <p class="text-sm text-gray-500">Industry experts</p>
                </div>
              </div>
            </div>
          </div>

        </div>
      </div>
    </section>

    <!-- Gallery Section -->
    <section id="gallery" class="py-24 bg-[#fafafc] relative z-10">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="text-center mb-16 space-y-4">
          <div class="inline-block px-4 py-1.5 bg-[#ff2e96]/5 border border-[#ff2e96]/10 rounded-full">
            <span class="text-[#ff2e96] text-xs font-bold uppercase tracking-[0.3em]">Gallery</span>
          </div>
          <h2 class="text-4xl sm:text-5xl font-black text-gray-900">Capturing the <span
              class="text-[#ff2e96]">Movement.</span></h2>
          <p class="text-gray-500 max-w-2xl mx-auto">Explore the vibrant energy and artistic expression inside our
            studios.</p>
        </div>

        <!-- Masonry-style Grid -->
        <div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4 auto-rows-[200px]">
          <div v-for="(item, index) in gallery" :key="item.id"
            class="group relative rounded-3xl overflow-hidden cursor-pointer" :class="[
              index === 0 ? 'md:col-span-2 md:row-span-2' : '',
              index === 1 ? 'md:row-span-2' : '',
              index === 4 ? 'md:col-span-2' : ''
            ]">
            <img :src="item.image" :alt="item.title"
              class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110">
            <!-- Overlay -->
            <div
              class="absolute inset-0 bg-gradient-to-t from-black/80 via-black/20 to-transparent opacity-0 group-hover:opacity-100 transition-all duration-500 flex flex-col justify-end p-8">
              <span
                class="text-white text-xl font-black tracking-tight transform translate-y-4 group-hover:translate-y-0 transition-transform duration-500 delayed-100">
                {{ item.title }}
              </span>
              <span
                class="text-[#ff2e96] text-xs font-bold uppercase tracking-widest transform translate-y-4 group-hover:translate-y-0 transition-transform duration-500 delayed-200">
                Studio Session
              </span>
            </div>
          </div>
        </div>

        <div class="mt-16 text-center">
          <a href="https://www.instagram.com/adamsdancestudio/" target="_blank"
            class="inline-block px-10 py-4 border-2 border-[#ff2e96] text-[#ff2e96] font-bold rounded-2xl hover:bg-[#ff2e96] hover:text-white transition-all duration-300">
            Follow more on Instagram
          </a>
        </div>
      </div>
    </section>

    <!-- Reviews Section -->
    <section id="reviews" class="py-24 bg-white relative z-10">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="text-center mb-16 space-y-4">
          <div class="inline-block px-4 py-1.5 bg-[#ff2e96]/5 border border-[#ff2e96]/10 rounded-full">
            <span class="text-[#ff2e96] text-xs font-bold uppercase tracking-[0.3em]">Testimonials</span>
          </div>
          <h2 class="text-4xl sm:text-5xl font-black text-gray-900">What Our <span class="text-[#ff2e96]">Dancers
              Say.</span></h2>
          <p class="text-gray-500 max-w-2xl mx-auto">Join a community built on passion, confidence, and pure joy.</p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
          <div v-for="review in reviews" :key="review.id"
            class="p-8 bg-[#fafafc] rounded-[2.5rem] border border-black/5 hover:border-[#ff2e96]/20 transition-all duration-300 group shadow-sm hover:shadow-xl hover:-translate-y-2">
            <!-- Stars -->
            <div class="flex gap-1 mb-6">
              <svg v-for="star in 5" :key="star" xmlns="http://www.w3.org/2000/svg"
                class="h-5 w-5 text-yellow-400 fill-current" viewBox="0 0 20 20">
                <path
                  d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
              </svg>
            </div>

            <p class="text-gray-600 text-lg leading-relaxed mb-8 italic">
              "{{ review.text }}"
            </p>

            <div class="flex items-center gap-4">
              <div
                class="w-12 h-12 rounded-full bg-gradient-to-tr from-[#ff2e96] to-purple-500 flex items-center justify-center text-white font-bold">
                {{ review.name[0] }}
              </div>
              <div>
                <h4 class="font-bold text-gray-900 leading-tight">{{ review.name }}</h4>
                <p class="text-sm text-gray-500">{{ review.role }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="py-24 bg-[#fafafc] relative z-10">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="grid grid-cols-1 lg:grid-cols-2 gap-16">

          <!-- Contact Info -->
          <div class="space-y-12">
            <div class="space-y-4">
              <div class="inline-block px-4 py-1.5 bg-[#ff2e96]/5 border border-[#ff2e96]/10 rounded-full">
                <span class="text-[#ff2e96] text-xs font-bold uppercase tracking-[0.3em]">Contact Us</span>
              </div>
              <h2 class="text-4xl sm:text-5xl font-black text-gray-900 leading-tight">
                Get in <span class="text-[#ff2e96]">Touch.</span>
              </h2>
              <p class="text-gray-500 text-lg">Have questions? We'd love to hear from you. Send us a message and we'll
                respond as soon as possible.</p>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-12">
              <!-- New Cairo Branch -->
              <div class="space-y-4">
                <div
                  class="w-12 h-12 rounded-2xl bg-white shadow-sm border border-black/5 flex items-center justify-center text-[#ff2e96]">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24"
                    stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                      d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" />
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                      d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
                  </svg>
                </div>
                <h3 class="font-bold text-gray-900 text-xl">New Cairo Branch</h3>
                <p class="text-gray-600 leading-relaxed">208 Mohammed Nagib Axis, First New Cairo, Cairo Governorate,
                  Egypt</p>
                <a href="tel:01005555137" class="inline-block font-bold text-[#ff2e96] hover:underline">01005555137</a>
              </div>

              <!-- Sheikh Zayed Branch -->
              <div class="space-y-4">
                <div
                  class="w-12 h-12 rounded-2xl bg-white shadow-sm border border-black/5 flex items-center justify-center text-purple-600">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24"
                    stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                      d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" />
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                      d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
                  </svg>
                </div>
                <h3 class="font-bold text-gray-900 text-xl">Sheikh Zayed Branch</h3>
                <p class="text-gray-600 leading-relaxed">Sheikh Zayed, Galleria 40 mall, First floor, Culture lab</p>
                <a href="tel:01030000131" class="inline-block font-bold text-purple-600 hover:underline">01030000131</a>
              </div>
            </div>

            <div class="pt-8 border-t border-black/5 space-y-6">
              <div class="flex items-center gap-4 group cursor-pointer">
                <div
                  class="w-10 h-10 rounded-xl bg-white shadow-sm border border-black/5 flex items-center justify-center text-gray-400 group-hover:text-[#ff2e96] transition-colors">
                  <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24"
                    stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                      d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
                  </svg>
                </div>
                <span class="text-gray-600 font-medium italic">info@adamsdancestudio.com</span>
              </div>

              <!-- Social Links -->
              <div class="flex items-center gap-6 pt-4">
                <a href="https://maps.google.com/?cid=6301208518536799205" target="_blank"
                  class="text-sm font-bold text-gray-400 hover:text-[#ff2e96] uppercase tracking-widest transition-colors">
                  Google Places
                </a>
                <a href="https://www.facebook.com/adamsdancestudio/" target="_blank"
                  class="text-sm font-bold text-gray-400 hover:text-[#ff2e96] uppercase tracking-widest transition-colors">
                  Facebook
                </a>
                <a href="https://www.instagram.com/adamsdancestudio/" target="_blank"
                  class="text-sm font-bold text-gray-400 hover:text-[#ff2e96] uppercase tracking-widest transition-colors">
                  Instagram
                </a>
              </div>
            </div>
          </div>

          <!-- Contact Form -->
          <div class="bg-white p-8 sm:p-12 rounded-[3rem] shadow-xl border border-black/5">
            <form class="space-y-6">
              <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div class="space-y-2">
                  <label class="text-xs font-bold text-gray-400 uppercase tracking-widest px-1">Name</label>
                  <input type="text" placeholder="Your Name"
                    class="w-full px-6 py-4 bg-[#fafafc] border border-black/5 rounded-2xl focus:outline-none focus:ring-2 focus:ring-[#ff2e96]/20 transition-all">
                </div>
                <div class="space-y-2">
                  <label class="text-xs font-bold text-gray-400 uppercase tracking-widest px-1">Email</label>
                  <input type="email" placeholder="email@example.com"
                    class="w-full px-6 py-4 bg-[#fafafc] border border-black/5 rounded-2xl focus:outline-none focus:ring-2 focus:ring-[#ff2e96]/20 transition-all">
                </div>
              </div>

              <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div class="space-y-2">
                  <label class="text-xs font-bold text-gray-400 uppercase tracking-widest px-1">Phone</label>
                  <input type="tel" placeholder="010..."
                    class="w-full px-6 py-4 bg-[#fafafc] border border-black/5 rounded-2xl focus:outline-none focus:ring-2 focus:ring-[#ff2e96]/20 transition-all">
                </div>
                <div class="space-y-2">
                  <label class="text-xs font-bold text-gray-400 uppercase tracking-widest px-1">Address</label>
                  <input type="text" placeholder="Your Address"
                    class="w-full px-6 py-4 bg-[#fafafc] border border-black/5 rounded-2xl focus:outline-none focus:ring-2 focus:ring-[#ff2e96]/20 transition-all">
                </div>
              </div>

              <div class="space-y-2">
                <label class="text-xs font-bold text-gray-400 uppercase tracking-widest px-1">Subject</label>
                <input type="text" placeholder="What's this about?"
                  class="w-full px-6 py-4 bg-[#fafafc] border border-black/5 rounded-2xl focus:outline-none focus:ring-2 focus:ring-[#ff2e96]/20 transition-all">
              </div>

              <div class="space-y-2">
                <label class="text-xs font-bold text-gray-400 uppercase tracking-widest px-1">Message</label>
                <textarea rows="4" placeholder="Type your message here..."
                  class="w-full px-6 py-4 bg-[#fafafc] border border-black/5 rounded-2xl focus:outline-none focus:ring-2 focus:ring-[#ff2e96]/20 transition-all resize-none"></textarea>
              </div>

              <button
                class="w-full py-5 bg-gray-900 text-white font-bold rounded-2xl hover:bg-gray-800 transition-all duration-300 transform active:scale-[0.98] shadow-lg shadow-black/10 flex items-center justify-center gap-3 group">
                Submit Message
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 group-hover:translate-x-1 transition-transform"
                  fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3" />
                </svg>
              </button>
            </form>
          </div>

        </div>
      </div>
    </section>

    <!-- Footer Section -->
    <footer class="bg-gray-900 pt-32 pb-16 px-4 sm:px-6 lg:px-8 overflow-hidden relative">
      <!-- Decorative -->
      <div class="absolute top-0 right-0 w-96 h-96 bg-[#ff2e96]/10 rounded-full blur-[150px]"></div>

      <div class="max-w-7xl mx-auto">
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-16 mb-24 reveal">
          <!-- Brand -->
          <div class="space-y-10">
            <a href="#home" class="flex items-center gap-4">
              <div
                class="w-14 h-14 bg-gradient-to-tr from-[#ff2e96] to-[#9240f4] rounded-2xl flex items-center justify-center p-3 shadow-xl shadow-pink-500/10">
                <svg viewBox="0 0 24 24" fill="none" class="w-full h-full stroke-white stroke-[2.5]"
                  stroke-linecap="round" stroke-linejoin="round">
                  <path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5" />
                </svg>
              </div>
              <span class="text-white font-black text-2xl uppercase tracking-tighter">ADAM'S<br><span
                  class="text-[#ff2e96]">DANCE.</span></span>
            </a>
            <p class="text-gray-400 text-lg leading-relaxed">
              Elevating the art of dance in Cairo for over 6 years. Join our passionate community and find your rhythm.
            </p>
            <div class="flex gap-4">
              <a href="https://www.facebook.com/adamsdancestudio/" target="_blank"
                class="w-12 h-12 rounded-xl bg-white/5 border border-white/10 flex items-center justify-center text-white hover:bg-[#ff2e96] hover:border-[#ff2e96] transition-all group">
                <span class="sr-only">Facebook</span>
                <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5 group-hover:scale-110 transition-transform"
                  fill="currentColor" viewBox="0 0 24 24">
                  <path
                    d="M9 8h-3v4h3v12h5v-12h3.642l.358-4h-4v-1.667c0-.955.192-1.333 1.115-1.333h2.885v-5h-3.808c-3.596 0-5.192 1.583-5.192 4.615v3.385z" />
                </svg>
              </a>
              <a href="https://www.instagram.com/adamsdancestudio/" target="_blank"
                class="w-12 h-12 rounded-xl bg-white/5 border border-white/10 flex items-center justify-center text-white hover:bg-[#ff2e96] hover:border-[#ff2e96] transition-all group">
                <span class="sr-only">Instagram</span>
                <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5 group-hover:scale-110 transition-transform"
                  fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                  viewBox="0 0 24 24">
                  <rect x="2" y="2" width="20" height="20" rx="5" ry="5"></rect>
                  <path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"></path>
                  <line x1="17.5" y1="6.5" x2="17.51" y2="6.5"></line>
                </svg>
              </a>
              <a href="https://maps.google.com/?cid=6301208518536799205" target="_blank"
                class="w-12 h-12 rounded-xl bg-white/5 border border-white/10 flex items-center justify-center text-white hover:bg-[#ff2e96] hover:border-[#ff2e96] transition-all group">
                <span class="sr-only">Google Maps</span>
                <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5 group-hover:scale-110 transition-transform"
                  fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                  viewBox="0 0 24 24">
                  <path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"></path>
                  <circle cx="12" cy="10" r="3"></circle>
                </svg>
              </a>
            </div>
          </div>

          <!-- Quick Links -->
          <div>
            <h4 class="text-white font-black text-xl mb-10 uppercase tracking-widest">Navigation</h4>
            <ul class="space-y-6">
              <li v-for="link in navLinks" :key="link.id">
                <a :href="'#' + link.id"
                  class="text-gray-400 hover:text-white transition-all duration-300 font-medium text-lg flex items-center gap-3 group">
                  <span
                    class="w-1.5 h-1.5 rounded-full bg-[#ff2e96] scale-0 group-hover:scale-100 transition-all"></span>
                  {{ link.name }}
                </a>
              </li>
            </ul>
          </div>

          <!-- Branches -->
          <div>
            <h4 class="text-white font-black text-xl mb-10 uppercase tracking-widest">Our Studios</h4>
            <div class="space-y-8">
              <div class="group">
                <div
                  class="text-gray-100 font-black text-sm uppercase tracking-widest mb-2 group-hover:text-[#ff2e96] transition-colors">
                  NEW CAIRO</div>
                <p class="text-gray-400 text-sm leading-relaxed">208 Mohammed Nagib Axis, First New Cairo</p>
              </div>
              <div class="group">
                <div
                  class="text-gray-100 font-black text-sm uppercase tracking-widest mb-2 group-hover:text-purple-500 transition-colors">
                  SHEIKH ZAYED</div>
                <p class="text-gray-400 text-sm leading-relaxed">Galleria 40 mall, First floor, Culture lab</p>
              </div>
            </div>
          </div>

          <!-- Newsletter -->
          <div class="space-y-8">
            <h4 class="text-white font-black text-xl uppercase tracking-widest">Stay Updated</h4>
            <p class="text-gray-400 text-sm">Join our newsletter for class updates and events.</p>
            <div class="relative group">
              <input type="email" placeholder="Email Address"
                class="w-full bg-white/5 border border-white/10 rounded-2xl py-4 px-6 text-white text-sm focus:outline-none focus:border-[#ff2e96]/50 transition-all">
              <button
                class="absolute top-1 right-1 bottom-1 px-5 bg-white text-black rounded-xl font-black text-[10px] uppercase hover:bg-[#ff2e96] hover:text-white transition-all">JOIN</button>
            </div>
          </div>
        </div>

        <div class="pt-16 border-t border-white/5 flex flex-col md:flex-row justify-between items-center gap-8">
          <p class="text-gray-500 text-sm font-medium">© 2024 Adam's Dance Studio. All rights reserved.</p>
          <div class="flex gap-8">
            <a href="#"
              class="text-gray-500 hover:text-white text-[10px] uppercase font-black tracking-widest transition-colors">Privacy
              Policy</a>
            <a href="#"
              class="text-gray-500 hover:text-white text-[10px] uppercase font-black tracking-widest transition-colors">Terms
              of Service</a>
          </div>
        </div>
      </div>

      <!-- Scroll to Top -->
      <button @click="scrollToTop"
        class="absolute bottom-12 right-12 w-16 h-16 rounded-full bg-[#ff2e96] text-white flex items-center justify-center shadow-2xl shadow-pink-500/20 hover:scale-110 active:scale-95 transition-all group z-20">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8 group-hover:-translate-y-1 transition-transform"
          fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M5 15l7-7 7 7" />
        </svg>
      </button>
    </footer>
  </div>
</template>

<style scoped>
.slide-up-enter-active,
.slide-up-leave-active {
  transition: all 0.6s cubic-bezier(0.16, 1, 0.3, 1);
}

.slide-up-enter-from {
  transform: translateY(100%);
  opacity: 0;
}

.slide-up-leave-to {
  transform: translateY(-100%);
  opacity: 0;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 1s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.reveal {
  opacity: 0;
  transform: translateY(30px);
  transition: all 1s cubic-bezier(0.16, 1, 0.3, 1);
}

.reveal-visible {
  opacity: 1;
  transform: translateY(0);
}

.mask-social {
  background-color: currentColor;
  mask-repeat: no-repeat;
  mask-position: center;
  mask-size: contain;
}

/* Custom transitions for better performance */
img {
  content-visibility: auto;
}

/* Smooth Scroll Fix for Safari/Other browsers */
@media (prefers-reduced-motion: no-preference) {
  :root {
    scroll-behavior: smooth;
  }
}

/* Slide Up Text Animation Delay */
.delayed-100 {
  transition-delay: 100ms;
}

.delayed-200 {
  transition-delay: 200ms;
}
</style>
