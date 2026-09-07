<template>
  <div class="app-container">
    <Login v-if="!isLoggedIn" @login-success="handleLoginSuccess" />
    <Dashboard v-else :username="username" @logout="handleLogout" />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Login from './components/Login.vue'
import Dashboard from './components/Dashboard.vue'

const isLoggedIn = ref(false)
const username = ref('')

const handleLoginSuccess = (user) => {
  isLoggedIn.value = true
  username.value = user
}

const handleLogout = () => {
  isLoggedIn.value = false
  username.value = ''
}
</script>

<style scoped>
.app-container {
  min-height: 100vh;
}
</style>