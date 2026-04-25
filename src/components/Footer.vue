<script setup>
const year = new Date().getFullYear();
</script>

<template>
  <footer class="py-20 px-[5%] md:px-[10%] bg-[var(--card-bg)] border-t border-[var(--border-color)]">
    <div class="max-w-[1400px] mx-auto">
      <div class="flex flex-col md:flex-row justify-between items-center mb-16 gap-8">
        <div class="flex flex-col items-center md:items-start gap-4">
          <span class="text-4xl md:text-5xl font-black tracking-tighter text-[var(--text-color)]">AHMAD.</span>
          <span class="text-[var(--text-muted)] max-w-sm text-center md:text-left">
            Elevating digital experiences with modern web technologies and exceptional design.
          </span>
        </div>
        <div class="flex gap-8 text-sm font-bold uppercase tracking-[2px] text-[var(--text-color)] opacity-70">
          <a href="#about" class="hover:text-accent hover:opacity-100 transition-colors">About</a>
          <a href="#work" class="hover:text-accent hover:opacity-100 transition-colors">Work</a>
          <a href="#contact" class="hover:text-accent hover:opacity-100 transition-colors">Contact</a>
        </div>
      </div>
      
      <div class="flex flex-col md:flex-row justify-between items-center pt-8 border-t border-[var(--border-color)] text-xs text-[var(--text-muted)] uppercase tracking-widest gap-4">
        <p>&copy; {{ year }} Ahmad Ali. All Rights Reserved.</p>
        <div class="flex flex-wrap items-center justify-center gap-4">
          <span>Built with Vue.js</span>
          <span class="text-accent">&bull;</span>
          <span>Tailwind CSS</span>
        </div>
      </div>
    </div>
  </footer>
</template>

