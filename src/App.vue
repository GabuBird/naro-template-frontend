<script setup lang="ts">
import { useRouter } from 'vue-router'

const router = useRouter()

const logout = async () => {
  // ログアウトAPIを叩く
  const res = await fetch('/api/logout', {
    method: 'POST'
  })

  // 成功したらログインページへリダイレクト
  if (res.ok) {
    router.push('/login')
  } else {
    alert('Logout failed')
  }
}
</script>

<template>
  <main>
    <div :class="$style.container">
      <header :class="$style.header">
        <router-link to="/">Home</router-link>
        |
        <router-link to="/ping">Ping</router-link>
        |
        <router-link to="/city/Tokyo">Tokyo</router-link>
        |
        <router-link to="/login">Login</router-link>
        |
        <router-link to="/countries">Countries</router-link>
        |
        <button @click="logout" :class="$style.logoutButton">Logout</button>
      </header>

      <router-view />
    </div>
  </main>
</template>

<style module>
.container {
  max-width: fit-content;
  margin: auto;
}
.header {
  display: flex;
  justify-content: center;
  align-items: center; /* ボタンとリンクの高さを揃える */
  gap: 0.5rem; /* 項目間のスペース */
}
/* リンクのように見えるボタンのスタイルを追加 */
.logoutButton {
  background: none;
  border: none;
  color: hsla(160, 100%, 37%, 1);
  cursor: pointer;
  text-decoration: underline;
  font-size: inherit;
  font-family: inherit;
  padding: 0;
}
</style>