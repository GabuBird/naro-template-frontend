<script setup lang="ts">
import { ref, onMounted } from 'vue'

const countries = ref()
onMounted(async () => {
  const res = await fetch('/api/countries')
  if (res.ok) {
    countries.value = await res.json()
  }
})
</script>

<template>
  <div>
    <h1>Countries</h1>
    <ul v-if="countries">
      <li v-for="country in countries" :key="country.code">
        <router-link :to="`/countries/${country.code}/cities`">{{ country.name }}</router-link>
      </li>
    </ul>
    <div v-else>国が見つかりませんでした</div>
  </div>
</template>