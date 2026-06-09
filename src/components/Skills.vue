<script setup>
import { ref } from 'vue'

const skills = ref([
  { name: 'HTML/CSS', level: 90 },
  { name: 'JavaScript', level: 85 },
  { name: 'Vue.js', level: 80 },
  { name: 'Spring Boot', level: 75 },
  { name: 'MySQL', level: 70 },
  { name: 'Python', level: 65 }
])

const animatedLevels = ref(skills.value.map(() => 0))

const animateProgress = () => {
  skills.value.forEach((skill, index) => {
    let current = 0
    const increment = skill.level / 50
    const timer = setInterval(() => {
      current += increment
      if (current >= skill.level) {
        animatedLevels.value[index] = skill.level
        clearInterval(timer)
      } else {
        animatedLevels.value[index] = Math.floor(current)
      }
    }, 20)
  })
}

const sectionRef = ref(null)
const observer = new IntersectionObserver(
  (entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        animateProgress()
        observer.disconnect()
      }
    })
  },
  { threshold: 0.3 }
)

import { onMounted, onUnmounted } from 'vue'
onMounted(() => {
  if (sectionRef.value) {
    observer.observe(sectionRef.value)
  }
})

onUnmounted(() => {
  observer.disconnect()
})
</script>

<template>
  <section id="skills" ref="sectionRef" class="skills-section">
    <div class="section-content">
      <h3>技术技能</h3>
      <div class="skills-grid">
        <div v-for="(skill, index) in skills" :key="index" class="skill-card">
          <div class="skill-header">
            <span>{{ skill.name }}</span>
            <span>{{ animatedLevels[index] }}%</span>
          </div>
          <el-progress :percentage="animatedLevels[index]" :stroke-width="16" :show-text="false" />
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.skills-section {
  padding: 4rem 2rem;
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

.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1.5rem;
  margin-top: 2rem;
}

.skill-card {
  background: white;
  padding: 1.5rem;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.skill-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.1);
}

.skill-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 0.5rem;
  font-weight: bold;
  color: #333;
}

.el-progress-bar__outer {
  background: #f0f0f0;
  border-radius: 8px;
}

.el-progress-bar__inner {
  border-radius: 8px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
}

@media (max-width: 768px) {
  .skills-grid {
    grid-template-columns: 1fr;
  }
}
</style>