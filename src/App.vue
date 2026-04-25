<script setup>
import { onMounted, ref } from 'vue';
import Lenis from 'lenis';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
import Navbar from './components/Navbar.vue';
import Hero from './components/Hero.vue';
import About from './components/About.vue';
import Projects from './components/Projects.vue';
import Contact from './components/Contact.vue';
import Footer from './components/Footer.vue';

gsap.registerPlugin(ScrollTrigger);

const canvasRef = ref(null);

onMounted(() => {
  // Smooth scroll
  const lenis = new Lenis({
    duration: 1.2,
    easing: (t) => Math.min(1, 1.001 - Math.pow(2, -10 * t)),
    smoothWheel: true,
  });

  function raf(time) {
    lenis.raf(time);
    requestAnimationFrame(raf);
  }

  requestAnimationFrame(raf);
  lenis.on('scroll', ScrollTrigger.update);
  gsap.ticker.add((time) => lenis.raf(time * 1000));
  gsap.ticker.lagSmoothing(0);

  // Global Blockchain Node Network Animation
  const canvas = canvasRef.value;
  const ctx = canvas.getContext('2d');
  let width, height;
  let nodes = [];
  const mouse = { x: null, y: null };

  const resize = () => {
    width = canvas.width = window.innerWidth;
    height = canvas.height = window.innerHeight;
  };
  window.addEventListener('resize', resize);
  resize();

  window.addEventListener('mousemove', (e) => {
    mouse.x = e.clientX;
    mouse.y = e.clientY;
  });

  class Node {
    constructor() {
      this.x = Math.random() * width;
      this.y = Math.random() * height;
      this.vx = (Math.random() - 0.5) * 1.5;
      this.vy = (Math.random() - 0.5) * 1.5;
      this.radius = Math.random() * 2 + 1;
    }
    
    update() {
      this.x += this.vx;
      this.y += this.vy;
      
      if (this.x < 0 || this.x > width) this.vx = -this.vx;
      if (this.y < 0 || this.y > height) this.vy = -this.vy;

      // Mouse interaction (slight attraction for "blockchain" interconnected feel)
      if (mouse.x != null && mouse.y != null) {
        let dx = mouse.x - this.x;
        let dy = mouse.y - this.y;
        let distance = Math.sqrt(dx * dx + dy * dy);
        if (distance < 150) {
          this.x += dx * 0.01;
          this.y += dy * 0.01;
        }
      }
      this.draw();
    }
    
    draw() {
      const isLight = document.documentElement.getAttribute('data-theme') === 'light';
      ctx.beginPath();
      ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
      ctx.fillStyle = isLight ? 'rgba(0, 179, 95, 0.8)' : 'rgba(0, 255, 136, 0.8)';
      ctx.fill();
    }
  }

  const initNodes = () => {
    nodes = [];
    let count = window.innerWidth > 768 ? 100 : 40; // Dense network
    for (let i = 0; i < count; i++) {
      nodes.push(new Node());
    }
  };
  initNodes();

  const connectNodes = () => {
    const isLight = document.documentElement.getAttribute('data-theme') === 'light';
    const rgb = isLight ? '0, 179, 95' : '0, 255, 136';
    
    for (let i = 0; i < nodes.length; i++) {
      for (let j = i; j < nodes.length; j++) {
        let dx = nodes[i].x - nodes[j].x;
        let dy = nodes[i].y - nodes[j].y;
        let distance = dx * dx + dy * dy;
        
        // Connect if close enough
        if (distance < 20000) {
          ctx.beginPath();
          ctx.strokeStyle = `rgba(${rgb}, ${1 - distance/20000})`;
          ctx.lineWidth = 0.5;
          ctx.moveTo(nodes[i].x, nodes[i].y);
          ctx.lineTo(nodes[j].x, nodes[j].y);
          ctx.stroke();
        }
      }
      
      // Connect to mouse
      if (mouse.x != null && mouse.y != null) {
        let dx = nodes[i].x - mouse.x;
        let dy = nodes[i].y - mouse.y;
        let distance = dx * dx + dy * dy;
        if (distance < 25000) {
          ctx.beginPath();
          ctx.strokeStyle = `rgba(${rgb}, ${1 - distance/25000})`;
          ctx.lineWidth = 1;
          ctx.moveTo(nodes[i].x, nodes[i].y);
          ctx.lineTo(mouse.x, mouse.y);
          ctx.stroke();
        }
      }
    }
  };

  const animate = () => {
    ctx.clearRect(0, 0, width, height);
    for (let i = 0; i < nodes.length; i++) {
      nodes[i].update();
    }
    connectNodes();
    requestAnimationFrame(animate);
  };
  animate();
});
</script>

<template>
  <div class="app-container relative">
    <canvas ref="canvasRef" class="fixed inset-0 w-full h-full pointer-events-none z-0 opacity-40"></canvas>
    
    <div class="relative z-10">
      <Navbar />
      <main>
        <Hero />
        <About />
        <Projects />
        <Contact />
      </main>
      <Footer />
    </div>
  </div>
</template>

<style>
.app-container {
  width: 100%;
  position: relative;
}
</style>
