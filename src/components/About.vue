<script setup>
</script>

<template>
  <section id="about" class="about-section">
    <el-row :gutter="20">
      <el-col :span="12">
        <div class="section-card">
          <h3>关于我</h3>
          <p>我是常州大学软件工程专业的一名学生，对前端开发和后端开发都有浓厚的兴趣。喜欢学习新技术，解决实际问题。</p>
          <p>在校期间积极参与项目开发，获得了丰富的实践经验。希望未来能够成为一名优秀的全栈工程师。</p>
        </div>
      </el-col>
      <el-col :span="12">
        <div class="section-card">
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
  </section>
</template>

<style scoped>
.about-section {
  padding: 4rem 2rem;
  background: #f8f9fa;
}

.section-card {
  background: white;
  padding: 2rem;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
  height: 100%;
}

.section-card h3 {
  font-size: 1.5rem;
  margin-bottom: 1.5rem;
  color: #333;
  position: relative;
  padding-bottom: 0.5rem;
}

.section-card h3::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 50px;
  height: 3px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  border-radius: 2px;
}

.section-card p {
  color: #666;
  line-height: 1.8;
  margin-bottom: 1rem;
}

.el-timeline-item__content {
  padding: 1rem 0;
}

.el-timeline-item__content h4 {
  color: #333;
  margin-bottom: 0.5rem;
}

.el-timeline-item__content p {
  margin-bottom: 0.3rem;
}
</style>