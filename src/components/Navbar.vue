<script setup>
import { onMounted, ref } from 'vue';
import gsap from 'gsap';
import { Moon, Sun } from 'lucide-vue-next';

const navLinks = [
  { name: 'About', href: '#about' },
  { name: 'Work', href: '#work' },
  { name: 'Contact', href: '#contact' }
];

const isLight = ref(false);

const toggleTheme = () => {
  isLight.value = !isLight.value;
  if (isLight.value) {
    document.documentElement.setAttribute('data-theme', 'light');
  } else {
    document.documentElement.removeAttribute('data-theme');
  }
};

onMounted(() => {
  // Check system preference
  if (window.matchMedia && window.matchMedia('(prefers-color-scheme: light)').matches) {
    // isLight.value = true;
    // document.documentElement.setAttribute('data-theme', 'light');
  }

  gsap.from('.nav-item', {
    y: -20,
    opacity: 0,
    duration: 1,
    stagger: 0.1,
    ease: 'power4.out',
    delay: 0.5
  });
});
</script>

<template>
  <nav class="fixed top-0 left-0 w-full px-[5%] py-6 z-[100] backdrop-blur-sm bg-[var(--bg-color)]/80 border-b border-[var(--border-color)]">
    <div class="flex justify-between items-center max-w-[1400px] mx-auto">
      <div class="nav-item">
        <span class="text-2xl font-extrabold tracking-tighter text-[var(--text-color)]">AHMAD.</span>
      </div>
      <div class="flex items-center gap-8 md:gap-12">
        <div class="hidden md:flex gap-8">
          <a v-for="link in navLinks" 
             :key="link.name" 
             :href="link.href" 
             class="nav-link nav-item text-sm font-bold uppercase tracking-[2px] text-[var(--text-color)] relative hover:text-accent transition-colors duration-300">
            {{ link.name }}
          </a>
        </div>
        
        <button @click="toggleTheme" 
                class="nav-item relative p-3 rounded-full border border-[var(--border-color)] bg-[var(--card-blur)] hover:border-accent hover:shadow-[0_0_15px_rgba(0,255,136,0.3)] transition-all duration-300 text-[var(--text-color)] overflow-hidden flex items-center justify-center group"
                title="Toggle Theme">
          <span class="absolute inset-0 bg-accent/10 opacity-0 group-hover:opacity-100 transition-opacity"></span>
          <div class="transition-transform duration-500 ease-[cubic-bezier(0.68,-0.55,0.265,1.55)]" :class="isLight ? 'rotate-[360deg] scale-100' : 'rotate-0 scale-100'">
            <Sun v-if="!isLight" :size="20" class="text-accent drop-shadow-[0_0_5px_rgba(0,255,136,0.5)]" />
            <Moon v-else :size="20" class="text-accent drop-shadow-[0_0_5px_rgba(0,255,136,0.5)]" />
          </div>
        </button>
      </div>
    </div>
  </nav>
</template>

<style scoped>
@reference "../style.css";

.nav-link::after {
  content: '';
  @apply absolute -bottom-1 left-0 w-0 h-[2px] bg-accent transition-all duration-300;
}

.nav-link:hover::after {
  @apply w-full;
}
</style>
