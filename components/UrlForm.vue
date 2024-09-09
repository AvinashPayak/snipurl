<template>
    <section class="container mt-10">
      <div class="card">
        <form>
          <div class="flex gap-5 items-end">
            <div class="w-5/12">
              <label for="url" class="text-white">Long URL</label>
              <input type="text" name="url" id="url" />
            </div>
            <div class="w-5/12">
              <label for="shortkey" class="text-white">Short Key</label>
              <input type="text" name="shortkey" id="shortkey" />
            </div>
            <div class="w-2/12">
                <button class="btn-primary py-3 rounded-xl w-full">Short</button>
            </div>
          </div>
        </form>
      </div>
    </section>
</template>