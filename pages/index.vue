<template>
  <section class="h-screen grid place-content-center">
    <div class="max-w-3xl mx-auto text-center">
      <h1 class="text-5xl font-bold heading">
        Snip your URLs and make them easy to share with SnipURL!
      </h1>
      <p class="my-10 text-lg w-10/12 md:w-2/3 mx-auto">
        Transform your long URLs into short shareable links with SnipURL
      </p>
      <NuxtLink
      class="btn btn-primary"
        :to="{
          name: 'dashboard',
        }"
        >Short Now!</NuxtLink
      >
    </div>
  </section>
</template>

<style scoped>
.heading {
  background: linear-gradient(180deg, #fff 0%, rgba(255, 255, 255, 0) 189%);
  background-clip: text;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}
</style>
