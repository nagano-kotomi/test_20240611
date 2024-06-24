<!-- <script setup>
import TheWelcome from '../components/TheWelcome.vue'
</script>

<template>
  <main>
    <TheWelcome />
  </main>
</template> -->

<template>
  <div>
    <h1>Home Page</h1>
    <RouterLink to="/learn">Go to Learn</RouterLink>
  </div>
</template>

<script>
export default {
  name: 'Home'
}
</script>

<style scoped>
/* 任意のスタイルを追加 */
</style>
