<script setup>
import { ref } from 'vue'

const projects = ref([
  {
    id: 1,
    title: '校园二手交易平台',
    description: '基于Vue和Spring Boot开发的校园二手商品交易系统，支持在线聊天和支付功能。',
    technologies: ['Vue3', 'Element Plus', 'Spring Boot', 'MySQL'],
    image: 'https://neeko-copilot.bytedance.net/api/text_to_image?prompt=modern%20e-commerce%20platform%20interface%20design%20with%20clean%20UI&image_size=landscape_16_9'
  },
  {
    id: 2,
    title: '智能天气助手',
    description: '实时天气预报应用，提供精准的天气数据和穿衣建议。',
    technologies: ['React', 'Node.js', 'OpenWeather API'],
    image: 'https://neeko-copilot.bytedance.net/api/text_to_image?prompt=weather%20app%20interface%20with%20beautiful%20sky%20background&image_size=landscape_16_9'
  },
  {
    id: 3,
    title: '在线代码编辑器',
    description: '支持多种编程语言的在线代码编辑器，实时预览运行结果。',
    technologies: ['Vue3', 'Monaco Editor', 'Docker'],
    image: 'https://neeko-copilot.bytedance.net/api/text_to_image?prompt=code%20editor%20interface%20with%20syntax%20highlighting&image_size=landscape_16_9'
  }
])

const activeProject = ref(null)
</script>

<template>
  <section id="projects" class="projects-section">
    <div class="section-content">
      <h3>我的项目</h3>
      <div class="projects-grid">
        <el-card 
          v-for="project in projects" 
          :key="project.id" 
          class="project-card"
          @mouseenter="activeProject = project.id"
          @mouseleave="activeProject = null"
        >
          <template #header>
            <div class="project-header">
              <h4>{{ project.title }}</h4>
            </div>
          </template>
          <div class="project-image">
            <img :src="project.image" :alt="project.title" />
          </div>
          <div class="project-content">
            <p>{{ project.description }}</p>
            <div class="project-tech">
              <el-tag v-for="(tech, techIndex) in project.technologies" :key="techIndex" size="small">
                {{ tech }}
              </el-tag>
            </div>
          </div>
          <div :class="['project-overlay', { 'overlay-active': activeProject === project.id }]">
            <el-button type="primary">查看详情</el-button>
          </div>
        </el-card>
      </div>
    </div>
  </section>
</template>

<style scoped>
.projects-section {
  padding: 4rem 2rem;
  background: #f8f9fa;
}

.section-content {
  max-width: 1200px;
  margin: 0 auto;
}

.section-content h3 {
  text-align: center;
  font-size: 2rem;
  margin-bottom: 2rem;
  color: #333;
  position: relative;
  padding-bottom: 0.5rem;
}

.section-content h3::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 50px;
  height: 3px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  border-radius: 2px;
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 2rem;
  margin-top: 2rem;
}

.project-card {
  height: 100%;
  overflow: hidden;
  position: relative;
  transition: transform 0.3s ease;
}

.project-card:hover {
  transform: translateY(-8px);
}

.project-header {
  padding: 1rem;
}

.project-header h4 {
  font-size: 1.2rem;
  color: #333;
  margin: 0;
}

.project-image {
  height: 180px;
  overflow: hidden;
}

.project-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.project-card:hover .project-image img {
  transform: scale(1.05);
}

.project-content {
  padding: 1rem;
}

.project-content p {
  color: #666;
  font-size: 0.9rem;
  line-height: 1.6;
}

.project-tech {
  margin-top: 1rem;
}

.project-tech .el-tag {
  margin-right: 0.5rem;
  margin-bottom: 0.5rem;
}

.project-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(102, 126, 234, 0.9);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.overlay-active {
  opacity: 1;
}

.project-overlay .el-button {
  background: white;
  color: #667eea;
  border: none;
}

.project-overlay .el-button:hover {
  background: #f0f0f0;
}

@media (max-width: 768px) {
  .projects-grid {
    grid-template-columns: 1fr;
  }
}
</style>