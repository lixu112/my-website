
<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

// 暗黑模式
const isDark = ref(false)
const toggleDark = () => {
  isDark.value = !isDark.value
  document.documentElement.classList.toggle('dark', isDark.value)
}

// 技能列表数据
const skills = ref([
  { name: 'HTML/CSS', level: 90, color: '#e34c26' },
  { name: 'JavaScript', level: 85, color: '#f7df1e' },
  { name: 'Vue.js', level: 80, color: '#42b883' },
  { name: 'Spring Boot', level: 75, color: '#6db33f' },
  { name: 'MySQL', level: 70, color: '#00758f' },
  { name: 'Python', level: 65, color: '#3776ab' }
])

// 项目列表数据
const projects = ref([
  {
    title: '校园二手交易平台',
    description: '基于Vue和Spring Boot开发的校园二手商品交易系统，支持在线聊天和支付功能。',
    technologies: ['Vue3', 'Element Plus', 'Spring Boot', 'MySQL'],
    image: 'https://trae-api-cn.mchost.guru/api/ide/v1/text_to_image?prompt=online%20marketplace%20platform%20website%20modern%20clean%20ui&image_size=landscape_16_9'
  },
  {
    title: '智能天气助手',
    description: '实时天气预报应用，提供精准的天气数据和穿衣建议。',
    technologies: ['React', 'Node.js', 'OpenWeather API'],
    image: 'https://trae-api-cn.mchost.guru/api/ide/v1/text_to_image?prompt=weather%20app%20dashboard%20modern%20clean%20ui&image_size=landscape_16_9'
  }
])

// 导航项
const navItems = [
  { id: 'home', label: '首页' },
  { id: 'about', label: '关于我' },
  { id: 'skills', label: '技能' },
  { id: 'projects', label: '项目' },
  { id: 'contact', label: '联系方式' }
]

// 当前激活的导航
const activeNav = ref('home')

// 平滑滚动到指定区域
const scrollTo = (id) => {
  const element = document.getElementById(id)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
    activeNav.value = id
  }
}

// 监听滚动更新导航高亮
const handleScroll = () => {
  const sections = navItems.map(item => ({
    id: item.id,
    element: document.getElementById(item.id)
  }))
  
  const scrollPosition = window.scrollY + 100
  
  for (let i = sections.length - 1; i >= 0; i--) {
    const section = sections[i]
    if (section.element && section.element.offsetTop <= scrollPosition) {
      activeNav.value = section.id
      break
    }
  }
  
  // 显示/隐藏返回顶部按钮
  showBackTop.value = window.scrollY > 300
}

// 返回顶部
const showBackTop = ref(false)
const backToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

// 挂载和卸载时添加/移除滚动监听
onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
  <!-- 导航栏 -->
  <header class="header" id="home">
    <div class="header-content">
      <h1 class="logo">我的空间</h1>
      <nav class="nav">
        <a 
          v-for="item in navItems" 
          :key="item.id"
          :class="['nav-link', { active: activeNav === item.id }]"
          @click="scrollTo(item.id)"
        >
          {{ item.label }}
        </a>
        <el-switch
          v-model="isDark"
          @change="toggleDark"
          active-text="🌙"
          inactive-text="☀️"
          inline-prompt
          class="dark-switch"
        />
      </nav>
    </div>
  </header>

  <!-- 英雄区域 -->
  <section class="hero">
    <div class="hero-content">
      <div class="hero-avatar">
        <div class="avatar-circle">
          <span>LX</span>
        </div>
      </div>
      <h2 class="hero-title">你好，我是 <span class="highlight">lx</span></h2>
      <p class="hero-subtitle">常州大学 · 软件工程专业 · 大三学生</p>
      <p class="hero-desc">热爱编程，专注于Web全栈开发</p>
      <el-button type="primary" size="large" class="hero-btn" @click="scrollTo('about')">
        了解更多
        <el-icon class="el-icon--right"><ArrowDown /></el-icon>
      </el-button>
    </div>
    <div class="hero-wave">
      <svg viewBox="0 0 1440 120" preserveAspectRatio="none">
        <path d="M0,60 C360,120 720,0 1080,60 C1260,90 1350,30 1440,60 L1440,120 L0,120 Z" fill="currentColor"/>
      </svg>
    </div>
  </section>

  <!-- 关于我 -->
  <section class="section" id="about">
    <h3 class="section-title">关于我</h3>
    <el-row :gutter="40">
      <el-col :xs="24" :sm="24" :md="12" :lg="12">
        <div class="about-card fade-in">
          <div class="about-icon">👨‍💻</div>
          <h4>个人简介</h4>
          <p>我是常州大学软件工程专业的一名学生，对前端开发和后端开发都有浓厚的兴趣。喜欢学习新技术，解决实际问题。</p>
          <p>在校期间积极参与项目开发，获得了丰富的实践经验。希望未来能够成为一名优秀的全栈工程师。</p>
        </div>
      </el-col>
      <el-col :xs="24" :sm="24" :md="12" :lg="12">
        <div class="about-card fade-in">
          <div class="about-icon">🎓</div>
          <h4>教育背景</h4>
          <el-timeline>
            <el-timeline-item timestamp="2021-至今" placement="top" color="#667eea">
              <h4>常州大学</h4>
              <p>软件工程专业 · 本科</p>
              <p class="course">主修课程：数据结构、操作系统、计算机网络、数据库原理</p>
            </el-timeline-item>
          </el-timeline>
        </div>
      </el-col>
    </el-row>
  </section>

  <!-- 技能展示 -->
  <section class="section skills-section" id="skills">
    <h3 class="section-title">技术技能</h3>
    <div class="skills-grid">
      <div 
        v-for="(skill, index) in skills" 
        :key="index" 
        class="skill-card fade-in"
        :style="{ animationDelay: `${index * 0.1}s` }"
      >
        <div class="skill-icon" :style="{ background: skill.color }">
          {{ skill.name.charAt(0) }}
        </div>
        <div class="skill-info">
          <div class="skill-header">
            <span class="skill-name">{{ skill.name }}</span>
            <span class="skill-level">{{ skill.level }}%</span>
          </div>
          <el-progress 
            :percentage="skill.level" 
            :stroke-width="8"
            :color="skill.color"
          />
        </div>
      </div>
    </div>
  </section>

  <!-- 项目展示 -->
  <section class="section projects-section" id="projects">
    <h3 class="section-title">我的项目</h3>
    <div class="projects-grid">
      <el-card 
        v-for="(project, index) in projects" 
        :key="index" 
        class="project-card fade-in"
        :body-style="{ padding: '0' }"
        :style="{ animationDelay: `${index * 0.15}s` }"
      >
        <div class="project-image">
          <img :src="project.image" :alt="project.title" />
          <div class="project-overlay">
            <el-button type="primary" round>查看详情</el-button>
          </div>
        </div>
        <div class="project-content">
          <h4>{{ project.title }}</h4>
          <p>{{ project.description }}</p>
          <div class="project-tech">
            <el-tag 
              v-for="(tech, techIndex) in project.technologies" 
              :key="techIndex" 
              size="small"
              effect="light"
            >
              {{ tech }}
            </el-tag>
          </div>
        </div>
      </el-card>
    </div>
  </section>

  <!-- 联系方式 -->
  <section class="section contact-section" id="contact">
    <h3 class="section-title">联系方式</h3>
    <div class="contact-grid">
      <div class="contact-item fade-in">
        <div class="contact-icon">📧</div>
        <span>邮箱</span>
      </div>
      <div class="contact-item fade-in">
        <div class="contact-icon">📱</div>
        <span>微信</span>
      </div>
      <div class="contact-item fade-in">
        <div class="contact-icon">🐙</div>
        <span>GitHub</span>
      </div>
      <div class="contact-item fade-in">
        <div class="contact-icon">📝</div>
        <span>掘金</span>
      </div>
    </div>
  </section>

  <!-- 页脚 -->
  <footer class="footer">
    <p>© 2024 我的个人网站. 保留所有权利.</p>
    <div class="social-links">
      <el-button link>GitHub</el-button>
      <el-button link>掘金</el-button>
      <el-button link>知乎</el-button>
      <el-button link>邮箱</el-button>
    </div>
  </footer>

  <!-- 返回顶部按钮 -->
  <transition name="fade">
    <el-button 
      v-show="showBackTop"
      class="back-top"
      type="primary"
      circle
      size="large"
      @click="backToTop"
    >
      <el-icon><ArrowUp /></el-icon>
    </el-button>
  </transition>
</template>

<style>
/* CSS变量 */
:root {
  --primary-color: #667eea;
  --secondary-color: #764ba2;
  --accent-color: #f5576c;
  --bg-color: #ffffff;
  --bg-secondary: #f5f7fa;
  --text-color: #333333;
  --text-secondary: #666666;
  --card-bg: #ffffff;
  --shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
}

.dark {
  --primary-color: #8b9cf4;
  --secondary-color: #9b6bb8;
  --accent-color: #f5576c;
  --bg-color: #1a1a2e;
  --bg-secondary: #16213e;
  --text-color: #e4e4e4;
  --text-secondary: #a0a0a0;
  --card-bg: #252542;
  --shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
}

/* 全局样式 */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
}

body {
  font-family: 'Microsoft YaHei', -apple-system, BlinkMacSystemFont, sans-serif;
  line-height: 1.6;
  color: var(--text-color);
  background: var(--bg-color);
  transition: background 0.3s, color 0.3s;
}

/* 动画 */
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

@keyframes float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-10px); }
}

.fade-in {
  animation: fadeInUp 0.6s ease forwards;
  opacity: 0;
}

/* 导航栏 */
.header {
  background: linear-gradient(135deg, var(--primary-color) 0%, var(--secondary-color) 100%);
  padding: 0.8rem 0;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  box-shadow: 0 2px 20px rgba(0, 0, 0, 0.15);
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
  font-size: 1.6rem;
  font-weight: bold;
  letter-spacing: 1px;
}

.nav {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.nav-link {
  color: rgba(255, 255, 255, 0.85);
  text-decoration: none;
  padding: 0.5rem 1rem;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.3s ease;
  font-size: 0.95rem;
}

.nav-link:hover,
.nav-link.active {
  color: white;
  background: rgba(255, 255, 255, 0.2);
}

.dark-switch {
  margin-left: 1rem;
}

/* 英雄区域 */
.hero {
  background: linear-gradient(135deg, var(--primary-color) 0%, var(--secondary-color) 50%, var(--accent-color) 100%);
  color: white;
  padding: 8rem 2rem 6rem;
  text-align: center;
  position: relative;
  overflow: hidden;
  margin-top: 60px;
}

.hero-content {
  max-width: 800px;
  margin: 0 auto;
  position: relative;
  z-index: 2;
}

.hero-avatar {
  margin-bottom: 1.5rem;
}

.avatar-circle {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.2);
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto;
  font-size: 2.5rem;
  font-weight: bold;
  border: 3px solid rgba(255, 255, 255, 0.5);
  animation: float 3s ease-in-out infinite;
}

.hero-title {
  font-size: 2.8rem;
  margin-bottom: 0.8rem;
  font-weight: 700;
}

.hero-title .highlight {
  background: linear-gradient(90deg, #ffd700, #ff6b6b);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.hero-subtitle {
  font-size: 1.3rem;
  margin-bottom: 0.5rem;
  opacity: 0.9;
}

.hero-desc {
  font-size: 1.1rem;
  margin-bottom: 2rem;
  opacity: 0.85;
}

.hero-btn {
  padding: 1rem 2.5rem;
  font-size: 1.1rem;
  border-radius: 50px;
  background: white;
  color: var(--primary-color);
  border: none;
  font-weight: 600;
  transition: all 0.3s ease;
}

.hero-btn:hover {
  transform: translateY(-3px);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
}

.hero-wave {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  color: var(--bg-color);
}

.hero-wave svg {
  width: 100%;
  height: 80px;
  display: block;
}

/* 通用区域样式 */
.section {
  padding: 5rem 2rem;
  max-width: 1200px;
  margin: 0 auto;
}

.section-title {
  text-align: center;
  font-size: 2.2rem;
  margin-bottom: 3rem;
  color: var(--text-color);
  position: relative;
}

.section-title::after {
  content: '';
  position: absolute;
  bottom: -10px;
  left: 50%;
  transform: translateX(-50%);
  width: 60px;
  height: 4px;
  background: linear-gradient(90deg, var(--primary-color), var(--secondary-color));
  border-radius: 2px;
}

/* 关于我 */
.about-card {
  background: var(--card-bg);
  padding: 2rem;
  border-radius: 16px;
  box-shadow: var(--shadow);
  height: 100%;
  margin-bottom: 2rem;
}

.about-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.about-card h4 {
  font-size: 1.3rem;
  margin-bottom: 1rem;
  color: var(--text-color);
}

.about-card p {
  color: var(--text-secondary);
  margin-bottom: 0.8rem;
  line-height: 1.8;
}

.about-card .course {
  font-size: 0.9rem;
}

/* 技能样式 */
.skills-section {
  background: var(--bg-secondary);
  max-width: 100%;
  padding-left: 2rem;
  padding-right: 2rem;
}

.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 1.5rem;
  max-width: 1200px;
  margin: 0 auto;
}

.skill-card {
  background: var(--card-bg);
  padding: 1.5rem;
  border-radius: 16px;
  box-shadow: var(--shadow);
  display: flex;
  align-items: center;
  gap: 1rem;
  transition: transform 0.3s ease;
}

.skill-card:hover {
  transform: translateY(-5px);
}

.skill-icon {
  width: 50px;
  height: 50px;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-weight: bold;
  font-size: 1.2rem;
  flex-shrink: 0;
}

.skill-info {
  flex: 1;
}

.skill-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 0.5rem;
}

.skill-name {
  font-weight: 600;
  color: var(--text-color);
}

.skill-level {
  color: var(--text-secondary);
  font-size: 0.9rem;
}

/* 项目样式 */
.projects-section {
  background: var(--bg-color);
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
  gap: 2rem;
}

.project-card {
  border-radius: 16px;
  overflow: hidden;
  box-shadow: var(--shadow);
  transition: transform 0.3s ease;
  background: var(--card-bg);
}

.project-card:hover {
  transform: translateY(-8px);
}

.project-image {
  position: relative;
  height: 200px;
  overflow: hidden;
}

.project-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}

.project-card:hover .project-image img {
  transform: scale(1.1);
}

.project-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.project-card:hover .project-overlay {
  opacity: 1;
}

.project-content {
  padding: 1.5rem;
}

.project-content h4 {
  font-size: 1.3rem;
  margin-bottom: 0.8rem;
  color: var(--text-color);
}

.project-content p {
  color: var(--text-secondary);
  margin-bottom: 1rem;
  line-height: 1.6;
}

.project-tech .el-tag {
  margin-right: 0.5rem;
  margin-bottom: 0.5rem;
}

/* 联系方式 */
.contact-section {
  background: var(--bg-secondary);
  max-width: 100%;
}

.contact-grid {
  display: flex;
  justify-content: center;
  gap: 2rem;
  flex-wrap: wrap;
}

.contact-item {
  background: var(--card-bg);
  padding: 1.5rem 2.5rem;
  border-radius: 16px;
  box-shadow: var(--shadow);
  text-align: center;
  cursor: pointer;
  transition: all 0.3s ease;
}

.contact-item:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.15);
}

.contact-icon {
  font-size: 2.5rem;
  margin-bottom: 0.5rem;
}

.contact-item span {
  color: var(--text-color);
  font-weight: 500;
}

/* 页脚样式 */
.footer {
  background: linear-gradient(135deg, #2c3e50 0%, #1a252f 100%);
  color: white;
  text-align: center;
  padding: 2.5rem;
}

.social-links {
  margin-top: 1rem;
}

.social-links .el-button {
  color: white !important;
  margin: 0 0.5rem;
}

.social-links .el-button:hover {
  color: var(--primary-color) !important;
}

/* 返回顶部 */
.back-top {
  position: fixed;
  right: 2rem;
  bottom: 2rem;
  z-index: 999;
  box-shadow: 0 4px 20px rgba(102, 126, 234, 0.4);
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

/* 响应式设计 */
@media (max-width: 768px) {
  .header-content {
    flex-direction: column;
    gap: 0.8rem;
    padding: 0 1rem;
  }

  .nav {
    flex-wrap: wrap;
    justify-content: center;
  }

  .nav-link {
    padding: 0.4rem 0.8rem;
    font-size: 0.85rem;
  }

  .dark-switch {
    margin-left: 0;
    margin-top: 0.5rem;
  }

  .hero {
    padding: 6rem 1rem 4rem;
    margin-top: 100px;
  }

  .hero-title {
    font-size: 2rem;
  }

  .hero-subtitle {
    font-size: 1rem;
  }

  .avatar-circle {
    width: 100px;
    height: 100px;
    font-size: 2rem;
  }

  .section {
    padding: 3rem 1rem;
  }

  .section-title {
    font-size: 1.8rem;
  }

  .projects-grid {
    grid-template-columns: 1fr;
  }

  .skills-grid {
    grid-template-columns: 1fr;
  }

  .contact-grid {
    gap: 1rem;
  }

  .contact-item {
    padding: 1rem 1.5rem;
  }

  .back-top {
    right: 1rem;
    bottom: 1rem;
  }
}
</style>
