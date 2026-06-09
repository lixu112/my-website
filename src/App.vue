
<script setup>
// 在这里可以定义响应式数据
import { ref } from 'vue'

// 技能列表数据
const skills = ref([
  { name: 'HTML/CSS', level: 90 },
  { name: 'JavaScript', level: 85 },
  { name: 'Vue.js', level: 80 },
  { name: 'Spring Boot', level: 75 },
  { name: 'MySQL', level: 70 },
  { name: 'Python', level: 65 }
])

// 项目列表数据
const projects = ref([
  {
    title: '校园二手交易平台',
    description: '基于Vue和Spring Boot开发的校园二手商品交易系统，支持在线聊天和支付功能。',
    technologies: ['Vue3', 'Element Plus', 'Spring Boot', 'MySQL'],
    image: '/src/assets/project1.jpg' // 你需要准备图片或使用在线图片链接
  },
  {
    title: '智能天气助手',
    description: '实时天气预报应用，提供精准的天气数据和穿衣建议。',
    technologies: ['React', 'Node.js', 'OpenWeather API'],
    image: '/src/assets/project2.jpg'
  }
])
</script>

<template>
  <!-- 导航栏 -->
  <el-row>
    <el-col :span="24">
      <div class="header">
        <div class="header-content">
          <h1 class="logo">我的空间</h1>
          <div class="nav">
            <el-button link type="primary">首页</el-button>
            <el-button link>关于我</el-button>
            <el-button link>技能</el-button>
            <el-button link>项目</el-button>
            <el-button link>联系方式</el-button>
          </div>
        </div>
      </div>
    </el-col>
  </el-row>

  <!-- 英雄区域 -->
  <el-row>
    <el-col :span="24">
      <div class="hero">
        <div class="hero-content">
          <h2>你好，我是 lx</h2>
          <p>常州大学 · 软件工程专业 · 大三学生</p>
          <p>热爱编程，专注于Web全栈开发</p>
          <el-button type="primary" size="large">了解更多</el-button>
        </div>
      </div>
    </el-col>
  </el-row>

  <!-- 关于我 -->
  <el-row :gutter="20">
    <el-col :span="12">
      <div class="section">
        <h3>关于我</h3>
        <p>我是常州大学软件工程专业的一名学生，对前端开发和后端开发都有浓厚的兴趣。喜欢学习新技术，解决实际问题。</p>
        <p>在校期间积极参与项目开发，获得了丰富的实践经验。希望未来能够成为一名优秀的全栈工程师。</p>
      </div>
    </el-col>
    <el-col :span="12">
      <div class="section">
        <h3>教育背景</h3>
        <el-timeline>
          <el-timeline-item timestamp="2021-至今" placement="top">
            <h4>常州大学</h4>
            <p>软件工程专业 · 本科</p>
            <p>主修课程：数据结构、操作系统、计算机网络、数据库原理</p>
          </el-timeline-item>
        </el-timeline>
      </div>
    </el-col>
  </el-row>

  <!-- 技能展示 -->
  <el-row>
    <el-col :span="24">
      <div class="section">
        <h3>技术技能</h3>
        <div class="skills">
          <div v-for="(skill, index) in skills" :key="index" class="skill-item">
            <div class="skill-header">
              <span>{{ skill.name }}</span>
              <span>{{ skill.level }}%</span>
            </div>
            <el-progress :percentage="skill.level" :stroke-width="16" />
          </div>
        </div>
      </div>
    </el-col>
  </el-row>

  <!-- 项目展示 -->
  <el-row>
    <el-col :span="24">
      <div class="section">
        <h3>我的项目</h3>
        <div class="projects">
          <el-card v-for="(project, index) in projects" :key="index" class="project-card">
            <template #header>
              <div class="project-header">
                <h4>{{ project.title }}</h4>
              </div>
            </template>
            <div class="project-content">
              <p>{{ project.description }}</p>
              <div class="project-tech">
                <el-tag v-for="(tech, techIndex) in project.technologies" :key="techIndex" size="small">
                  {{ tech }}
                </el-tag>
              </div>
            </div>
          </el-card>
        </div>
      </div>
    </el-col>
  </el-row>

  <!-- 页脚 -->
  <el-row>
    <el-col :span="24">
      <div class="footer">
        <p>© 2024 我的个人网站. 保留所有权利.</p>
        <div class="social-links">
          <el-button link>GitHub</el-button>
          <el-button link>掘金</el-button>
          <el-button link>知乎</el-button>
          <el-button link>邮箱</el-button>
        </div>
      </div>
    </el-col>
  </el-row>
</template>

<style>
/* 全局样式 */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Microsoft YaHei', sans-serif;
  line-height: 1.6;
  color: #333;
}

/* 布局样式 */
.header {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  padding: 1rem 0;
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.1);
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

.hero {
  background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
  color: white;
  padding: 4rem 0;
  text-align: center;
}

.hero-content h2 {
  font-size: 2.5rem;
  margin-bottom: 1rem;
}

.hero-content p {
  font-size: 1.2rem;
  margin-bottom: 1rem;
}

.section {
  padding: 3rem 2rem;
  max-width: 1200px;
  margin: 0 auto;
}

.section h3 {
  text-align: center;
  font-size: 2rem;
  margin-bottom: 2rem;
  color: #333;
}

/* 技能样式 */
.skills {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1.5rem;
  margin-top: 2rem;
}

.skill-item {
  background: white;
  padding: 1.5rem;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.skill-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 0.5rem;
  font-weight: bold;
}

/* 项目样式 */
.projects {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
  gap: 2rem;
  margin-top: 2rem;
}

.project-card {
  height: 100%;
  transition: transform 0.3s ease;
}

.project-card:hover {
  transform: translateY(-5px);
}

.project-header {
  padding: 1rem;
}

.project-content {
  padding: 1rem;
}

.project-tech {
  margin-top: 1rem;
}

.project-tech .el-tag {
  margin-right: 0.5rem;
  margin-bottom: 0.5rem;
}

/* 页脚样式 */
.footer {
  background: #2c3e50;
  color: white;
  text-align: center;
  padding: 2rem;
  margin-top: 3rem;
}

.social-links {
  margin-top: 1rem;
}

.social-links .el-button {
  color: white !important;
  margin: 0 0.5rem;
}

.social-links .el-button:hover {
  color: #3498db !important;
}

/* 响应式设计 */
@media (max-width: 768px) {
  .header-content {
    flex-direction: column;
    gap: 1rem;
  }
  
  .hero-content h2 {
    font-size: 2rem;
  }
  
  .projects {
    grid-template-columns: 1fr;
  }
  
  .skills {
    grid-template-columns: 1fr;
  }
}
</style>

<style scoped>
/* 这里可以写组件特有的样式 */
</style>