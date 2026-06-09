<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const isScrolled = ref(false)

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})

const scrollToSection = (sectionId) => {
  const element = document.getElementById(sectionId)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}
</script>

<template>
  <header :class="['header', { 'header-scrolled': isScrolled }]">
    <div class="header-content">
      <h1 class="logo">我的空间</h1>
      <nav class="nav">
        <el-button link type="primary" @click="scrollToSection('home')">首页</el-button>
        <el-button link @click="scrollToSection('about')">关于我</el-button>
        <el-button link @click="scrollToSection('skills')">技能</el-button>
        <el-button link @click="scrollToSection('projects')">项目</el-button>
        <el-button link @click="scrollToSection('contact')">联系方式</el-button>
      </nav>
    </div>
  </header>
</template>

<style scoped>
.header {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  padding: 1rem 0;
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  transition: all 0.3s ease;
}

.header-scrolled {
  padding: 0.5rem 0;
  background: rgba(102, 126, 234, 0.95);
  backdrop-filter: blur(10px);
}

.header-content {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 2rem;
}

.logo {
  color: white;
  font-size: 1.8rem;
  font-weight: bold;
}

.nav .el-button {
  color: white !important;
  margin-left: 1rem;
}

.nav .el-button:hover {
  color: #ffd04b !important;
}

@media (max-width: 768px) {
  .header-content {
    flex-direction: column;
    gap: 1rem;
  }
  
  .nav .el-button {
    margin-left: 0.5rem;
  }
}
</style>