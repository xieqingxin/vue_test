<template>
  <div class="dashboard-wrapper">
    <div class="dashboard-header">
      <div class="header-left">
        <h1>🎉 欢迎，{{ username }}！</h1>
      </div>
      <button class="logout-btn" @click="handleLogout">
        退出登录
      </button>
    </div>
    
    <div class="dashboard-content">
      <div class="welcome-card">
        <h2>登录成功</h2>
        <p>您已成功登录系统，祝您使用愉快！</p>
      </div>

      <div class="info-cards">
        <div class="info-card">
          <div class="card-icon">👤</div>
          <div class="card-info">
            <h3>当前用户</h3>
            <p>{{ username }}</p>
          </div>
        </div>
        <div class="info-card">
          <div class="card-icon">📅</div>
          <div class="card-info">
            <h3>登录时间</h3>
            <p>{{ currentTime }}</p>
          </div>
        </div>
        <div class="info-card">
          <div class="card-icon">🔐</div>
          <div class="card-info">
            <h3>登录状态</h3>
            <p class="status-online">在线</p>
          </div>
        </div>
      </div>

      <div class="test-accounts">
        <h3>📝 测试账号</h3>
        <ul>
          <li><strong>账号：</strong>admin <strong>密码：</strong>123456</li>
          <li><strong>账号：</strong>user <strong>密码：</strong>password</li>
          <li><strong>账号：</strong>maizi <strong>密码：</strong>maizi123</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const props = defineProps({
  username: {
    type: String,
    required: true
  }
})

const emit = defineEmits(['logout'])

const currentTime = ref('')
let timer = null

const updateTime = () => {
  const now = new Date()
  currentTime.value = now.toLocaleString('zh-CN')
}

onMounted(() => {
  updateTime()
  timer = setInterval(updateTime, 1000)
})

onUnmounted(() => {
  if (timer) {
    clearInterval(timer)
  }
})

const handleLogout = () => {
  emit('logout')
}
</script>

<style scoped>
.dashboard-wrapper {
  min-height: 100vh;
  background: #f5f7fa;
}

.dashboard-header {
  background: #fff;
  padding: 20px 40px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.06);
}

.header-left h1 {
  font-size: 24px;
  color: #333;
}

.logout-btn {
  padding: 10px 20px;
  background: #e74c3c;
  color: #fff;
  border: none;
  border-radius: 6px;
  font-size: 14px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.logout-btn:hover {
  background: #c0392b;
}

.dashboard-content {
  max-width: 1200px;
  margin: 0 auto;
  padding: 40px 20px;
}

.welcome-card {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: #fff;
  padding: 40px;
  border-radius: 16px;
  margin-bottom: 30px;
}

.welcome-card h2 {
  font-size: 32px;
  margin-bottom: 10px;
}

.welcome-card p {
  font-size: 16px;
  opacity: 0.9;
}

.info-cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 20px;
  margin-bottom: 30px;
}

.info-card {
  background: #fff;
  padding: 25px;
  border-radius: 12px;
  display: flex;
  align-items: center;
  gap: 20px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.06);
  transition: all 0.3s ease;
}

.info-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
}

.card-icon {
  font-size: 40px;
  width: 60px;
  height: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: #f5f7fa;
  border-radius: 12px;
}

.card-info h3 {
  font-size: 14px;
  color: #888;
  margin-bottom: 6px;
}

.card-info p {
  font-size: 18px;
  color: #333;
  font-weight: 600;
}

.status-online {
  color: #27ae60 !important;
}

.test-accounts {
  background: #fff;
  padding: 30px;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.06);
}

.test-accounts h3 {
  font-size: 18px;
  color: #333;
  margin-bottom: 20px;
}

.test-accounts ul {
  list-style: none;
  padding: 0;
}

.test-accounts li {
  padding: 12px 15px;
  background: #f8f9fa;
  border-radius: 6px;
  margin-bottom: 10px;
  color: #555;
}

.test-accounts li:last-child {
  margin-bottom: 0;
}

.test-accounts strong {
  color: #333;
}
</style>