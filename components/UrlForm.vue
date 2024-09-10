<template>
    <section class="container mt-10">
      <div class="card">
        <form @submit.prevent="handleUrlForm">
          <div class="flex gap-5 items-end">
            <div class="w-5/12">
              <label for="url" class="text-white">Long URL</label>
              <input type="text" name="url" id="url" v-model="form.url" />
            </div>
            <div class="w-5/12">
              <label for="shortkey" class="text-white">Short Key</label>
              <input type="text" name="shortkey" id="shortkey" v-model="form.shortkey" />
            </div>
            <div class="w-2/12">
                <button class="btn-primary py-3 rounded-xl w-full">Short</button>
            </div>
          </div>
        </form>
      </div>
    </section>
</template>

<script lang="ts" setup>
import { nanoid } from "nanoid";
import type { Database } from "~/database.types";
const form = reactive({
  url:"",
  shortkey:""
})
const client = useSupabaseClient<Database>()
const user = useSupabaseUser()

const handleUrlForm = async () => {
  try {
    const { data, error } = await client.from('links').insert({
      long_url: form.url,
      key: form.shortkey,
      user_id: user.value?.id
    })

    if(error) {
      alert(error.message)
      return
    }

      generateShortkey()
      form.url = ""
      alert("link created")

  } catch(error) {
    console.log("Error:", error)
  }
}
const generateShortkey = (length:number = 6): void => {
  form.shortkey = nanoid(length)
}
onMounted(() => {
  generateShortkey()
})
</script>