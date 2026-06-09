<script setup>
const currentYear = new Date().getFullYear()

const scrollToTop = () => {
  window.scrollTo({ top: 0, behavior: 'smooth' })
}
</script>

<template>
  <footer id="contact" class="footer">
    <div class="footer-content">
      <div class="footer-info">
        <h4>联系方式</h4>
        <div class="contact-info">
          <div class="contact-item">
            <span class="icon">📧</span>
            <span>lx@example.com</span>
          </div>
          <div class="contact-item">
            <span class="icon">📱</span>
            <span>138-xxxx-xxxx</span>
          </div>
          <div class="contact-item">
            <span class="icon">📍</span>
            <span>江苏省常州市</span>
          </div>
        </div>
      </div>
      <div class="social-links">
        <h4>社交链接</h4>
        <div class="links">
          <el-button link>GitHub</el-button>
          <el-button link>掘金</el-button>
          <el-button link>知乎</el-button>
          <el-button link>邮箱</el-button>
        </div>
      </div>
    </div>
    <div class="footer-bottom">
      <p>© {{ currentYear }} 我的个人网站. 保留所有权利.</p>
      <el-button link @click="scrollToTop" class="back-to-top">
        <span>↑ 返回顶部</span>
      </el-button>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  background: #2c3e50;
  color: white;
  padding: 3rem 2rem;
}

.footer-content {
  max-width: 1200px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
  margin-bottom: 2rem;
}

.footer-info h4,
.social-links h4 {
  font-size: 1.2rem;
  margin-bottom: 1rem;
  color: #fff;
}

.contact-info {
  display: flex;
  flex-direction: column;
  gap: 0.8rem;
}

.contact-item {
  display: flex;
  align-items: center;
  gap: 0.8rem;
}

.contact-item .icon {
  font-size: 1.2rem;
}

.social-links .links {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.social-links .el-button {
  color: white !important;
  padding: 0.5rem 1rem;
}

.social-links .el-button:hover {
  color: #3498db !important;
}

.footer-bottom {
  max-width: 1200px;
  margin: 0 auto;
  padding-top: 2rem;
  border-top: 1px solid rgba(255, 255, 255, 0.1);
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 1rem;
}

.footer-bottom p {
  margin: 0;
  color: #aaa;
}

.back-to-top {
  color: #3498db !important;
  font-size: 0.9rem;
}

.back-to-top:hover {
  color: #2980b9 !important;
}

@media (max-width: 768px) {
  .footer-content {
    grid-template-columns: 1fr;
  }
  
  .footer-bottom {
    flex-direction: column;
    text-align: center;
  }
}
</style>