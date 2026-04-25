<script setup>
import { onMounted } from 'vue';
import gsap from 'gsap';
import { ArrowDownRight, Sparkles } from 'lucide-vue-next';

onMounted(() => {
  const tl = gsap.timeline();
  
  // Background particles animation
  gsap.to('.hero-glow', {
    rotate: 360,
    duration: 20,
    repeat: -1,
    ease: 'linear'
  });

  // Diamond Animation
  gsap.to('.diamond-shape', {
    rotationY: 360,
    rotationZ: 45,
    duration: 10,
    repeat: -1,
    ease: 'linear',
    transformOrigin: 'center'
  });
  
  gsap.to('.diamond-shape', {
    y: 30,
    duration: 2,
    yoyo: true,
    repeat: -1,
    ease: 'sine.inOut'
  });

  tl.to('.preloader', {
    yPercent: -100,
    duration: 1.2,
    ease: 'power4.inOut',
    delay: 0.5
  })
  .from('.hero-badge', {
    y: 20,
    opacity: 0,
    duration: 0.8,
    ease: 'power3.out'
  }, '-=0.2')
  .from('.hero-title-word', {
    y: 100,
    opacity: 0,
    duration: 1.2,
    stagger: 0.1,
    ease: 'power4.out',
    rotation: 5,
    transformOrigin: 'left top'
  }, '-=0.5')
  .from('.diamond-container', {
    scale: 0,
    opacity: 0,
    rotation: -180,
    duration: 1.5,
    ease: 'elastic.out(1, 0.5)'
  }, '-=1')
  .from('.hero-sub', {
    opacity: 0,
    y: 20,
    duration: 1,
    ease: 'power3.out'
  }, '-=0.8')
  .from('.hero-cta-wrapper', {
    y: 30,
    opacity: 0,
    duration: 1,
    ease: 'power3.out'
  }, '-=0.8');

  // Mouse move parallax
  window.addEventListener('mousemove', (e) => {
    const x = (e.clientX / window.innerWidth - 0.5) * 20;
    const y = (e.clientY / window.innerHeight - 0.5) * 20;
    
    gsap.to('.parallax-bg', {
      x: x,
      y: y,
      duration: 1,
      ease: 'power2.out'
    });
  });

});
</script>

<template>
  <div class="preloader fixed inset-0 z-[999] bg-accent flex items-center justify-center">
    <div class="text-[var(--bg-color)] text-4xl font-black tracking-tighter">AHMAD ALI.</div>
  </div>

  <section class="min-h-screen flex items-center px-[5%] md:px-[10%] relative overflow-hidden bg-transparent pt-20">
    <!-- Premium Grid Background -->
    <div class="absolute inset-0 bg-[url('https://grainy-gradients.vercel.app/noise.svg')] opacity-20 mix-blend-overlay pointer-events-none z-10 dark:opacity-20 opacity-40"></div>
    <div class="absolute inset-0 bg-[linear-gradient(to_right,var(--border-color)_1px,transparent_1px),linear-gradient(to_bottom,var(--border-color)_1px,transparent_1px)] bg-[size:40px_40px] [mask-image:radial-gradient(ellipse_60%_50%_at_50%_50%,#000_70%,transparent_100%)] z-0"></div>

    <div class="max-w-[1400px] w-full z-20 relative parallax-bg flex flex-col md:flex-row items-center justify-between gap-12">
      <div class="flex-1">
        <div class="hero-badge inline-flex items-center gap-2 px-4 py-2 rounded-full border border-[var(--border-color)] bg-[var(--card-blur)] backdrop-blur-md mb-8">
          <Sparkles :size="16" class="text-accent" />
          <span class="text-xs font-medium tracking-[2px] uppercase text-[var(--text-color)]">Available for freelance work</span>
        </div>

        <div class="text-[clamp(4rem,12vw,10rem)] font-black leading-[0.85] tracking-tighter flex flex-wrap gap-x-6">
          <div class="overflow-hidden"><span class="hero-title-word block text-[var(--text-color)]">CREATIVE</span></div>
          <div class="overflow-hidden"><span class="hero-title-word block text-transparent bg-clip-text bg-gradient-to-r from-accent to-secondary-accent">MERN</span></div>
          <div class="overflow-hidden w-full"><span class="hero-title-word block text-[var(--text-color)]">DEVELOPER</span></div>
        </div>
        
        <div class="mt-12 flex flex-col items-start gap-8 border-t border-[var(--border-color)] pt-8">
          <p class="hero-sub text-xl md:text-2xl max-w-[500px] text-[var(--text-muted)] font-light leading-relaxed">
            Dynamic and results-driven MERN Stack Developer with 4+ years of hands-on experience building scalable, high-performance web applications.
          </p>

          <div class="hero-cta-wrapper flex flex-col sm:flex-row items-center gap-6">
            <a href="#work" class="premium-button group flex items-center gap-3">
              <span class="relative z-10 text-[var(--text-color)] group-hover:text-white dark:group-hover:text-black font-bold uppercase tracking-wider">View Work</span>
              <div class="w-8 h-8 rounded-full bg-[var(--text-color)]/10 flex items-center justify-center group-hover:bg-white transition-colors relative z-10">
                <ArrowDownRight :size="18" class="text-[var(--text-color)] dark:group-hover:text-black" />
              </div>
            </a>
          </div>
        </div>
      </div>

      <!-- Diamond Animation Container -->
      <div class="hidden lg:flex diamond-container w-[400px] h-[400px] relative items-center justify-center perspective-[1000px]">
        <div class="diamond-shape relative w-48 h-48 preserve-3d">
          <div class="absolute inset-0 border-4 border-accent shadow-[0_0_50px_rgba(0,255,136,0.6)] backdrop-blur-sm bg-accent/10 flex items-center justify-center rotate-45">
            <div class="w-32 h-32 border-4 border-secondary-accent shadow-[0_0_30px_rgba(0,212,255,0.6)]"></div>
          </div>
        </div>
      </div>
    </div>
    
  </section>
</template>

<style scoped>
.hero-title-word {
  will-change: transform, opacity;
}
.perspective-[1000px] {
  perspective: 1000px;
}
.preserve-3d {
  transform-style: preserve-3d;
}
</style>
