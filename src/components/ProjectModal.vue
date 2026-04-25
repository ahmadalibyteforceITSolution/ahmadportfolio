<script setup>
import { watch, onMounted, ref } from 'vue';
import gsap from 'gsap';
import { X, ExternalLink, Github, CheckCircle2, Circle } from 'lucide-vue-next';

const props = defineProps({
  project: {
    type: Object,
    default: null
  },
  isOpen: {
    type: Boolean,
    default: false
  }
});

const emit = defineEmits(['close']);
const modalRef = ref(null);

// Example process steps for the stepper
const processSteps = [
  { id: 1, title: 'Research & Strategy', description: 'Analyzing requirements and defining project architecture.' },
  { id: 2, title: 'UI/UX Design', description: 'Creating high-fidelity wireframes and interactive prototypes.' },
  { id: 3, title: 'Development', description: 'Building scalable frontend and robust backend APIs.' },
  { id: 4, title: 'Deployment & QA', description: 'Testing for performance and deploying to production.' }
];

watch(() => props.isOpen, (newVal) => {
  if (newVal) {
    document.body.style.overflow = 'hidden';
    const tl = gsap.timeline();
    
    tl.to(modalRef.value, {
      y: 0,
      opacity: 1,
      duration: 0.8,
      ease: 'power4.out',
      display: 'block'
    })
    .from('.modal-content > *', {
      y: 30,
      opacity: 0,
      stagger: 0.1,
      duration: 0.6,
      ease: 'power3.out'
    }, '-=0.4')
    .from('.stepper-item', {
      x: -20,
      opacity: 0,
      stagger: 0.1,
      duration: 0.5,
      ease: 'power2.out'
    }, '-=0.2');
  } else {
    document.body.style.overflow = '';
    gsap.to(modalRef.value, {
      y: '100%',
      opacity: 0,
      duration: 0.6,
      ease: 'power4.in',
      onComplete: () => {
        gsap.set(modalRef.value, { display: 'none' });
      }
    });
  }
});

const close = () => {
  emit('close');
};
</script>

<template>
  <div 
    ref="modalRef" 
    class="fixed inset-0 z-[1000] bg-dark-bg/95 backdrop-blur-xl overflow-y-auto hidden translate-y-full opacity-0"
  >
    <div class="min-h-screen flex flex-col pt-24 pb-20 px-[5%] md:px-[10%] relative">
      <!-- Close Button -->
      <button 
        @click="close" 
        class="absolute top-8 right-[5%] md:right-[10%] p-4 bg-white/5 border border-white/10 rounded-full hover:bg-accent hover:text-black transition-colors z-50 group"
      >
        <X :size="24" class="group-hover:rotate-90 transition-transform duration-300" />
      </button>

      <div v-if="project" class="max-w-[1200px] mx-auto w-full modal-content">
        <!-- Header -->
        <div class="mb-12">
          <div class="inline-flex items-center gap-2 px-4 py-2 rounded-full border border-accent/30 bg-accent/10 mb-6">
            <span class="text-xs font-bold tracking-[2px] uppercase text-accent">{{ project.category }}</span>
          </div>
          <h2 class="text-5xl md:text-8xl font-black uppercase tracking-tighter leading-[0.9] mb-6">
            {{ project.title }}
          </h2>
          <div class="flex gap-4">
            <a :href="project.link" target="_blank" class="flex items-center gap-2 text-white/80 hover:text-accent transition-colors">
              <ExternalLink :size="20" /> <span>Live Preview</span>
            </a>
            <a href="#" class="flex items-center gap-2 text-white/80 hover:text-accent transition-colors">
              <Github :size="20" /> <span>Source Code</span>
            </a>
          </div>
        </div>

        <!-- Featured Image -->
        <div class="w-full h-[40vh] md:h-[60vh] rounded-3xl overflow-hidden mb-16 relative group">
          <img :src="project.image" :alt="project.title" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-700">
          <div class="absolute inset-0 bg-black/20 group-hover:bg-transparent transition-colors duration-500"></div>
        </div>

        <div class="grid lg:grid-cols-[1fr,1.5fr] gap-20">
          <!-- Left: Stepper / Process -->
          <div class="bg-white/5 border border-white/10 rounded-3xl p-8 md:p-10">
            <h3 class="text-2xl font-bold mb-8 flex items-center gap-3">
              <span class="w-2 h-2 rounded-full bg-accent"></span>
              Development Process
            </h3>
            
            <div class="relative">
              <!-- Stepper Line -->
              <div class="absolute left-[11px] top-2 bottom-2 w-[2px] bg-white/10"></div>
              
              <div class="flex flex-col gap-8">
                <div v-for="(step, index) in processSteps" :key="step.id" class="stepper-item relative pl-10">
                  <!-- Stepper Icon -->
                  <div class="absolute left-0 top-1 w-6 h-6 rounded-full bg-dark-bg border-[2px] border-accent flex items-center justify-center z-10 shadow-[0_0_10px_rgba(0,255,136,0.5)]">
                    <div class="w-2 h-2 rounded-full bg-accent"></div>
                  </div>
                  
                  <div class="flex flex-col gap-2">
                    <span class="text-xs font-bold text-accent tracking-[2px] uppercase">Step 0{{ index + 1 }}</span>
                    <h4 class="text-xl font-bold text-white">{{ step.title }}</h4>
                    <p class="text-sm text-white/60 leading-relaxed">{{ step.description }}</p>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Right: Details -->
          <div class="flex flex-col gap-10">
            <div>
              <h3 class="text-3xl font-bold mb-6">Project Overview</h3>
              <p class="text-lg text-white/70 leading-relaxed mb-6">
                {{ project.title }} is a comprehensive platform built to handle complex user interactions with a seamless, highly-optimized user interface. The primary objective was to deliver a premium user experience while ensuring robust backend functionality and data security.
              </p>
              <p class="text-lg text-white/70 leading-relaxed">
                By leveraging the MERN stack, we achieved rapid iteration cycles and a highly scalable architecture that can support thousands of concurrent users without performance degradation.
              </p>
            </div>

            <div>
              <h3 class="text-2xl font-bold mb-6">Tech Stack & Features</h3>
              <div class="grid sm:grid-cols-2 gap-4">
                <div class="flex items-center gap-3 bg-white/5 p-4 rounded-xl border border-white/5 hover:border-white/20 transition-colors">
                  <CheckCircle2 :size="20" class="text-accent" />
                  <span class="font-medium text-white/80">React & Next.js</span>
                </div>
                <div class="flex items-center gap-3 bg-white/5 p-4 rounded-xl border border-white/5 hover:border-white/20 transition-colors">
                  <CheckCircle2 :size="20" class="text-accent" />
                  <span class="font-medium text-white/80">Node.js & Express</span>
                </div>
                <div class="flex items-center gap-3 bg-white/5 p-4 rounded-xl border border-white/5 hover:border-white/20 transition-colors">
                  <CheckCircle2 :size="20" class="text-accent" />
                  <span class="font-medium text-white/80">MongoDB & Redis</span>
                </div>
                <div class="flex items-center gap-3 bg-white/5 p-4 rounded-xl border border-white/5 hover:border-white/20 transition-colors">
                  <CheckCircle2 :size="20" class="text-accent" />
                  <span class="font-medium text-white/80">Tailwind CSS & Canvas</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
