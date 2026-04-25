<script setup>
import { onMounted } from 'vue';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
import { Code, Layout, Server, Database, Briefcase } from 'lucide-vue-next';

gsap.registerPlugin(ScrollTrigger);

const experiences = [
  { company: 'Venom Tech (Pvt. Ltd.)', role: 'MERN Stack Developer', duration: 'Feb 2024 – Mar 2026', desc: 'Designed responsive interfaces, optimized front-end performance by 20%, integrated REST/GraphQL APIs, and implemented state management using Redux.' },
  { company: 'Fabulous Technology Solution', role: 'MERN Stack Developer', duration: 'Aug 2024', desc: 'Developed a replica design process reducing time by 25%. Led a layout redesign that improved workflow and productivity by 15%.' },
  { company: 'Technology Brainz HR Consulting', role: 'Backend Developer', duration: 'Sep 2023', desc: 'Built browser-based React apps boosting engagement by 30%. Optimized REST API calls and reduced load times achieving a 15% speed increase.' }
];

const skillsChart = [
  { name: 'React / Next.js', level: 90 },
  { name: 'Node.js / Express', level: 85 },
  { name: 'MongoDB', level: 80 },
  { name: 'Vue.js', level: 75 },
  { name: 'TypeScript', level: 85 }
];

const techLogos = [
  { name: 'React', url: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/react/react-original.svg' },
  { name: 'Node.js', url: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/nodejs/nodejs-original.svg' },
  { name: 'MongoDB', url: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/mongodb/mongodb-original.svg' },
  { name: 'Next.js', url: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/nextjs/nextjs-original.svg' },
  { name: 'Express', url: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/express/express-original.svg' },
  { name: 'TailwindCSS', url: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/tailwindcss/tailwindcss-original.svg' },
  { name: 'TypeScript', url: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/typescript/typescript-original.svg' },
  { name: 'Docker', url: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/docker/docker-original.svg' },
  { name: 'Figma', url: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/figma/figma-original.svg' }
];

onMounted(() => {
  gsap.from('.about-anim', {
    scrollTrigger: {
      trigger: '.about-section',
      start: 'top 70%',
    },
    y: 50,
    opacity: 0,
    duration: 1,
    stagger: 0.1,
    ease: 'power3.out'
  });

  gsap.from('.skill-bar-fill', {
    scrollTrigger: {
      trigger: '.skills-chart-container',
      start: 'top 80%',
    },
    scaleX: 0,
    transformOrigin: 'left center',
    duration: 1.5,
    stagger: 0.1,
    ease: 'power4.out'
  });
});
</script>

<template>
  <section id="about" class="about-section py-32 px-[5%] md:px-[10%] bg-[var(--bg-color)] relative z-10">
    <div class="max-w-[1400px] mx-auto">
      
      <div class="mb-20 flex flex-col md:flex-row justify-between items-start md:items-end border-b border-[var(--border-color)] pb-8 gap-4 about-anim">
        <h2 class="text-6xl md:text-7xl font-black tracking-tight text-[var(--text-color)]">THE VISION</h2>
        <p class="text-accent font-semibold tracking-[2px] uppercase">01 / ABOUT ME</p>
      </div>

      <!-- Marquee Logos -->
      <div class="w-full overflow-hidden border-y border-[var(--border-color)] py-6 mb-20 about-anim flex whitespace-nowrap bg-[var(--card-blur)]">
        <div class="animate-marquee inline-flex items-center">
          <div v-for="tech in techLogos" :key="tech.name" class="flex items-center gap-4 mx-8 opacity-60 hover:opacity-100 transition-opacity cursor-default grayscale hover:grayscale-0">
            <img :src="tech.url" :alt="tech.name" class="w-10 h-10 object-contain">
            <span class="text-2xl font-bold uppercase tracking-widest text-[var(--text-color)]">{{ tech.name }}</span>
          </div>
        </div>
        <div class="animate-marquee inline-flex items-center" aria-hidden="true">
          <div v-for="tech in techLogos" :key="tech.name + '-copy'" class="flex items-center gap-4 mx-8 opacity-60 hover:opacity-100 transition-opacity cursor-default grayscale hover:grayscale-0">
            <img :src="tech.url" :alt="tech.name" class="w-10 h-10 object-contain">
            <span class="text-2xl font-bold uppercase tracking-widest text-[var(--text-color)]">{{ tech.name }}</span>
          </div>
        </div>
      </div>

      <div class="grid lg:grid-cols-[1fr,1.5fr] gap-20">
        <!-- Left: Experience Stepper -->
        <div class="flex flex-col gap-10 about-anim">
          <h3 class="text-3xl font-bold text-[var(--text-color)] flex items-center gap-3">
            <Briefcase class="text-accent" /> Work Experience
          </h3>
          
          <div class="relative pl-8 border-l border-[var(--border-color)] flex flex-col gap-12">
            <div v-for="(exp, index) in experiences" :key="index" class="relative">
              <div class="absolute -left-[41px] top-1 w-5 h-5 rounded-full bg-[var(--bg-color)] border-2 border-accent flex items-center justify-center shadow-[0_0_10px_rgba(0,255,136,0.5)]">
                <div class="w-2 h-2 rounded-full bg-accent"></div>
              </div>
              <span class="text-sm font-bold text-accent tracking-[2px] uppercase mb-2 block">{{ exp.duration }}</span>
              <h4 class="text-2xl font-bold text-[var(--text-color)]">{{ exp.role }}</h4>
              <p class="text-lg font-medium text-[var(--text-color)] opacity-70 mb-3">{{ exp.company }}</p>
              <p class="text-[var(--text-muted)] leading-relaxed">{{ exp.desc }}</p>
            </div>
          </div>
        </div>

        <!-- Right: Bio & Charts -->
        <div class="flex flex-col gap-16">
          <div class="text-xl text-[var(--text-muted)] leading-relaxed about-anim">
            <p class="mb-6">
              Dynamic and results-driven MERN Stack Developer with 4+ years of hands-on experience building scalable, high-performance web applications. Proven expertise in React.js, Node.js, MongoDB, and modern front-end frameworks. Strong track record of driving measurable improvements — from reducing load times by 20% to boosting user engagement by 30%.
            </p>
            <p class="text-lg opacity-70">
              Education: <span class="text-[var(--text-color)] font-bold">BS in Business & Information Technology</span>, University of the Punjab, Lahore (Sep 2020 – March 2024).
            </p>
          </div>

          <!-- Skills Chart -->
          <div class="skills-chart-container glass-card about-anim">
            <h3 class="text-2xl font-bold text-[var(--text-color)] mb-8">Technical Proficiency</h3>
            <div class="flex flex-col gap-6">
              <div v-for="skill in skillsChart" :key="skill.name" class="flex flex-col gap-2">
                <div class="flex justify-between text-sm font-medium text-[var(--text-color)]">
                  <span>{{ skill.name }}</span>
                  <span class="text-accent">{{ skill.level }}%</span>
                </div>
                <div class="w-full h-2 bg-[var(--border-color)] rounded-full overflow-hidden">
                  <div class="skill-bar-fill h-full bg-gradient-to-r from-accent to-secondary-accent rounded-full" :style="{ width: skill.level + '%' }"></div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
@keyframes marquee {
  0% { transform: translateX(0); }
  100% { transform: translateX(-100%); }
}

.animate-marquee {
  animation: marquee 20s linear infinite;
  padding-right: 2rem;
}
</style>
