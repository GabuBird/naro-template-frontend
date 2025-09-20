<script setup lang="ts">
import { ref, onMounted } from 'vue'
const props = defineProps<{ countryCode: string }>()
const cities = ref()
onMounted(async () => {
  const res = await fetch(`/api/countries/${props.countryCode}/cities`)
  if (res.ok) {
    cities.value = await res.json()
  }
})
</script>

<template>
  <div>
    <h1>Cities in {{ countryCode }}</h1>
    <ul v-if="cities">
      <li v-for="city in cities" :key="city.id">
        <router-link :to="`/city/${city.name.String}`">{{ city.name.String }}</router-link>
      </li>
    </ul>
    <div v-else>都市が見つかりませんでした</div>
  </div>
</template>