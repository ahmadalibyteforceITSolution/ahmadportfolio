<script setup>
import { onMounted } from 'vue';
import gsap from 'gsap';
import { Mail, Github, Linkedin, Send, Phone, MapPin } from 'lucide-vue-next';

onMounted(() => {
  gsap.from('.contact-anim', {
    scrollTrigger: {
      trigger: '.contact-section',
      start: 'top 80%'
    },
    y: 30,
    opacity: 0,
    duration: 1,
    stagger: 0.1,
    ease: 'power3.out'
  });
});
</script>

<template>
  <section id="contact" class="contact-section py-40 px-[5%] md:px-[10%] bg-[var(--card-bg)]">
    <div class="max-w-[1400px] mx-auto">
      <div class="grid lg:grid-cols-2 gap-20 items-center">
        <div>
          <h2 class="text-6xl md:text-8xl font-black leading-[0.9] tracking-tighter mb-8 contact-anim text-[var(--text-color)]">LET'S BUILD SOMETHING</h2>
          <p class="text-xl text-[var(--text-muted)] mb-12 max-w-md contact-anim">
            Whether you have a specific project in mind or just want to chat about tech, I'm always open to new opportunities.
          </p>
          
          <div class="flex flex-col gap-6 mb-12 contact-anim">
            <div class="flex items-center gap-4 text-[var(--text-color)] opacity-80 hover:opacity-100 hover:text-accent transition-colors cursor-pointer">
              <Mail :size="20" class="text-accent" />
              <span>ahmadalihafeez24@gmail.com</span>
            </div>
            <div class="flex items-center gap-4 text-[var(--text-color)] opacity-80 hover:opacity-100 hover:text-accent transition-colors cursor-pointer">
              <Phone :size="20" class="text-accent" />
              <span>+92 341 6887454</span>
            </div>
            <div class="flex items-center gap-4 text-[var(--text-color)] opacity-80">
              <MapPin :size="20" class="text-accent" />
              <span>Lahore, Pakistan</span>
            </div>
          </div>

          <div class="flex gap-6 contact-anim">
            <a href="https://linkedin.com/in/ch-ahmad-ali-016530243" target="_blank" class="p-4 rounded-full bg-[var(--bg-color)] border border-[var(--border-color)] hover:border-accent hover:text-accent text-[var(--text-color)] transition-all shadow-sm">
              <Linkedin :size="24" />
            </a>
            <a href="#" class="p-4 rounded-full bg-[var(--bg-color)] border border-[var(--border-color)] hover:border-accent hover:text-accent text-[var(--text-color)] transition-all shadow-sm">
              <Github :size="24" />
            </a>
          </div>
        </div>

        <form class="glass-card flex flex-col gap-8 contact-anim" @submit.prevent>
          <div class="flex flex-col gap-2">
            <label class="text-xs uppercase tracking-[2px] text-accent font-bold">Your Name</label>
            <input type="text" placeholder="John Doe" class="bg-[var(--bg-color)] border border-[var(--border-color)] p-4 rounded-xl text-[var(--text-color)] outline-none focus:border-accent transition-colors">
          </div>
          <div class="flex flex-col gap-2">
            <label class="text-xs uppercase tracking-[2px] text-accent font-bold">Email Address</label>
            <input type="email" placeholder="john@example.com" class="bg-[var(--bg-color)] border border-[var(--border-color)] p-4 rounded-xl text-[var(--text-color)] outline-none focus:border-accent transition-colors">
          </div>
          <div class="flex flex-col gap-2">
            <label class="text-xs uppercase tracking-[2px] text-accent font-bold">Message</label>
            <textarea rows="4" placeholder="Tell me about your project..." class="bg-[var(--bg-color)] border border-[var(--border-color)] p-4 rounded-xl text-[var(--text-color)] outline-none focus:border-accent transition-colors"></textarea>
          </div>
          <button type="submit" class="premium-button w-full flex items-center justify-center gap-2">
            <span class="relative z-10 font-bold uppercase tracking-widest text-[var(--text-color)] group-hover:text-black">Send Message</span> 
            <Send :size="18" class="relative z-10 text-accent group-hover:text-black" />
          </button>
        </form>
      </div>
    </div>
  </section>
</template>
