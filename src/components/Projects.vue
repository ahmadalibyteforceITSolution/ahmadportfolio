<script setup>
import { onMounted, ref } from 'vue';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
import { ExternalLink, ArrowRight, Activity, Code, Cpu, Box } from 'lucide-vue-next';
import ProjectModal from './ProjectModal.vue';

const projects = [
  { title: 'bytely.ai', category: 'Automation / AI / MERN', year: '2024', image: 'https://images.unsplash.com/photo-1677442136019-21780ecad995?auto=format&fit=crop&q=80&w=1000', link: 'https://bytely.ai' },
  { title: 'ezi.services', category: 'Home Services / Booking', year: '2024', image: 'https://images.unsplash.com/photo-1581578731548-c64695ce6958?auto=format&fit=crop&q=80&w=1000', link: 'https://ezi.services' },
  { title: 'venomtech.pk', category: 'Brand Portfolio', year: '2024', image: 'https://images.unsplash.com/photo-1451187580459-43490279c0fa?auto=format&fit=crop&q=80&w=1000', link: 'https://venomtech.pk' },
  { title: 'valeonglobal', category: 'Scheduler Platform', year: '2023', image: 'https://images.unsplash.com/photo-1507679799987-c73779587ccf?auto=format&fit=crop&q=80&w=1000', link: 'https://valeonglobal.com' },
  { title: 'lionsgatelimousine.com', category: 'Car Rental Store', year: '2023', image: 'https://images.unsplash.com/photo-1502877338535-766e1452684a?auto=format&fit=crop&q=80&w=1000', link: 'https://lionsgatelimousine.com' },
  { title: 'rivercitypaintingsa.com', category: 'Auto Retail', year: '2023', image: 'https://images.unsplash.com/photo-1603584173870-7f23fdae1b7a?auto=format&fit=crop&q=80&w=1000', link: 'https://rivercitypaintingsa.com' },
  { title: 'technoblick.com', category: 'Interactive Portfolio', year: '2023', image: 'https://images.unsplash.com/photo-1550745165-9bc0b252726f?auto=format&fit=crop&q=80&w=1000', link: 'https://technoblick.com' },
  { title: 'fabtechsol.com', category: 'Corporate Website', year: '2023', image: 'https://images.unsplash.com/photo-1497215728101-856f4ea42174?auto=format&fit=crop&q=80&w=1000', link: 'https://fabtechsol.com' },
  { title: 'gala-tab.app', category: 'Real Estate Updates', year: '2022', image: 'https://images.unsplash.com/photo-1560518883-ce09059eeffa?auto=format&fit=crop&q=80&w=1000', link: 'https://gala-tab.netlify.app' },
  { title: 'quaspect.com', category: 'Gaming Portfolio', year: '2022', image: 'https://images.unsplash.com/photo-1542751371-adc38448a05e?auto=format&fit=crop&q=80&w=1000', link: 'https://quaspect.com' },
  { title: 'shop.bytely.ai', category: 'E-commerce Store', year: '2024', image: 'https://images.unsplash.com/photo-1556742049-0cfed4f6a45d?auto=format&fit=crop&q=80&w=1000', link: 'https://shop.bytely.ai' },
  { title: 'wallpezia.com', category: 'Java Microservices', year: '2022', image: 'https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?auto=format&fit=crop&q=80&w=1000', link: 'https://wallpezia.com/wallpapers-and-ringtones' }
];

const selectedProject = ref(null);
const isModalOpen = ref(false);

const openProject = (project) => {
  selectedProject.value = project;
  isModalOpen.value = true;
};

const closeModal = () => {
  isModalOpen.value = false;
  setTimeout(() => {
    selectedProject.value = null;
  }, 600); // Wait for exit animation
};

onMounted(() => {
  // Fade in animation for each block as it scrolls into view
  const blocks = gsap.utils.toArray('.blockchain-block');
  
  blocks.forEach((block, i) => {
    gsap.from(block, {
      scrollTrigger: {
        trigger: block,
        start: 'top 85%',
      },
      y: 50,
      opacity: 0,
      duration: 0.8,
      ease: 'power3.out'
    });
  });

  // Animate the central blockchain line drawing downwards
  gsap.from('.blockchain-line-fill', {
    scrollTrigger: {
      trigger: '.projects-wrapper',
      start: 'top 50%',
      end: 'bottom 80%',
      scrub: 1
    },
    scaleY: 0,
    transformOrigin: 'top center',
    ease: 'none'
  });
});
</script>

<template>
  <section id="work" class="projects-wrapper py-32 bg-[var(--bg-color)] relative z-10">
    <div class="max-w-[1400px] mx-auto px-[5%] md:px-[10%]">
      
      <div class="mb-24 flex flex-col md:flex-row justify-between items-start md:items-end border-b border-[var(--border-color)] pb-8 gap-4">
        <h2 class="text-6xl md:text-7xl font-black tracking-tight text-[var(--text-color)] glow-text">THE LEDGER</h2>
        <p class="text-accent font-semibold tracking-[2px] uppercase flex items-center gap-2">
          <Box :size="20" /> 02 / BLOCKCHAIN WORK
        </p>
      </div>

      <!-- Vertical Blockchain Stepper Container -->
      <div class="relative w-full">
        <!-- Central Line (The Chain) -->
        <div class="absolute left-8 md:left-1/2 top-0 bottom-0 w-1 bg-[var(--border-color)] md:-translate-x-1/2 rounded-full hidden md:block">
          <div class="blockchain-line-fill w-full h-full bg-accent shadow-[0_0_15px_rgba(0,255,136,0.8)]"></div>
        </div>

        <div class="flex flex-col gap-24 relative z-10">
          <div v-for="(project, index) in projects" :key="project.title" class="blockchain-block flex flex-col md:flex-row items-center gap-8 md:gap-16 group" :class="index % 2 !== 0 ? 'md:flex-row-reverse' : ''">
            
            <!-- Block Data (Left or Right depending on odd/even) -->
            <div class="w-full md:w-1/2 flex flex-col" :class="index % 2 !== 0 ? 'md:items-start' : 'md:items-end md:text-right'">
              <div class="flex items-center gap-3 mb-4 text-xs font-mono text-[var(--text-muted)] tracking-widest uppercase bg-[var(--card-bg)] px-4 py-2 border border-[var(--border-color)] rounded-full">
                <Cpu :size="14" class="text-accent" />
                <span>BLOCK_{{ String(index + 1).padStart(3, '0') }}</span>
                <span class="w-1.5 h-1.5 rounded-full bg-accent animate-pulse"></span>
              </div>
              <h3 class="text-4xl md:text-5xl font-black uppercase tracking-tighter text-[var(--text-color)] mb-2 glow-text cursor-pointer hover:text-accent transition-colors" @click="openProject(project)">
                {{ project.title }}
              </h3>
              <p class="text-accent font-bold tracking-[2px] uppercase text-sm mb-6">{{ project.category }} — {{ project.year }}</p>
              
              <button @click="openProject(project)" class="flex items-center gap-2 text-[var(--text-muted)] hover:text-accent font-mono text-sm uppercase tracking-wider transition-colors">
                [ Inspect Block ] <ArrowRight :size="16" />
              </button>
            </div>

            <!-- Center Node Marker -->
            <div class="hidden md:flex absolute left-1/2 -translate-x-1/2 w-12 h-12 rounded-full border-2 border-accent bg-[var(--bg-color)] items-center justify-center shadow-[0_0_20px_rgba(0,255,136,0.2)] z-20 group-hover:scale-125 group-hover:shadow-[0_0_30px_rgba(0,255,136,0.5)] transition-all duration-300">
              <div class="w-4 h-4 rounded-full bg-accent animate-pulse"></div>
            </div>

            <!-- Block Visual (Image Card) -->
            <div class="w-full md:w-1/2">
              <div class="relative w-full aspect-[4/3] border border-[var(--border-color)] bg-[var(--card-bg)] backdrop-blur-md p-2 tech-card group-hover:border-accent transition-colors duration-500 cursor-pointer shadow-[0_0_30px_rgba(0,255,136,0.05)]" @click="openProject(project)">
                <!-- Corner Decorations -->
                <div class="absolute top-0 left-0 w-4 h-4 border-t-2 border-l-2 border-accent"></div>
                <div class="absolute top-0 right-0 w-4 h-4 border-t-2 border-r-2 border-accent"></div>
                <div class="absolute bottom-0 left-0 w-4 h-4 border-b-2 border-l-2 border-accent"></div>
                <div class="absolute bottom-0 right-0 w-4 h-4 border-b-2 border-r-2 border-accent"></div>

                <div class="relative w-full h-full overflow-hidden tech-image-mask">
                  <img :src="project.image" :alt="project.title" class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-110 filter grayscale-[50%] group-hover:grayscale-0">
                  <div class="absolute inset-0 bg-accent/20 mix-blend-overlay opacity-0 group-hover:opacity-100 transition-opacity duration-300"></div>
                </div>
              </div>
            </div>

          </div>
        </div>
      </div>

    </div>
  </section>

  <ProjectModal :isOpen="isModalOpen" :project="selectedProject" @close="closeModal" />
</template>

<style scoped>
.tech-card {
  clip-path: polygon(0 15px, 15px 0, 100% 0, 100% calc(100% - 15px), calc(100% - 15px) 100%, 0 100%);
}
.tech-image-mask {
  clip-path: polygon(0 10px, 10px 0, 100% 0, 100% calc(100% - 10px), calc(100% - 10px) 100%, 0 100%);
}
.glow-text {
  text-shadow: 0 0 15px rgba(0, 255, 136, 0.15);
}
</style>
