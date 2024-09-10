<template>
  <main class="pt-24">
    <section class="container">
      <h1 class="text-2xl font-bold text-white">Dashboard</h1>
    </section>
    <UrlForm />
    <LinkItem
      v-for="i in 5"
      :key="i"
      :link="{ shortKey: 'sdfgsdfg', longUrl: 'sdgdsg', id: '12' }"
    />
  </main>
</template>
<script lang="ts" setup>
definePageMeta({
  middleware: 'auth'
})
</script>
