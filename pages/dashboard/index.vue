<template>
  <main class="pt-24">
    <section class="container">
      <h1 class="text-2xl font-bold text-white">Dashboard</h1>
    </section>
    <UrlForm />
    <LinkItem
      v-for="link in data"
      :key="link.id"
      :link="{ shortKey: link.key, longUrl: link.long_url || '', id: link.id }"
    />
  </main>
</template>
<script lang="ts" setup>
import type { Database } from "~/database.types";

definePageMeta({
  middleware: "auth",
});

const client = useSupabaseClient<Database>()
const user = useSupabaseUser()

const { data } = useAsyncData("links", async () => {
  const { data, error } = await client
    .from("links")
    .select("*")
    .eq("user_id", user.value?.id)
    return data
});

console.log({data})
</script>
