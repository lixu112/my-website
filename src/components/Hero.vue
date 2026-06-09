<script setup>
const scrollToSection = (sectionId) => {
  const element = document.getElementById(sectionId)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}
</script>

<template>
  <section id="home" class="hero">
    <div class="hero-content">
      <h2>你好，我是 lx</h2>
      <p>常州大学 · 软件工程专业 · 大三学生</p>
      <p>热爱编程，专注于Web全栈开发</p>
      <el-button type="primary" size="large" @click="scrollToSection('about')">了解更多</el-button>
    </div>
  </section>
</template>

<style scoped>
.hero {
  background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
  color: white;
  padding: 6rem 0 4rem;
  text-align: center;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.hero-content h2 {
  font-size: 2.5rem;
  margin-bottom: 1rem;
  animation: fadeInUp 0.8s ease;
}

.hero-content p {
  font-size: 1.2rem;
  margin-bottom: 1rem;
  animation: fadeInUp 0.8s ease 0.2s both;
}

.hero-content .el-button {
  animation: fadeInUp 0.8s ease 0.4s both;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@media (max-width: 768px) {
  .hero-content h2 {
    font-size: 2rem;
  }
  
  .hero {
    padding: 5rem 0 3rem;
  }
}
</style>