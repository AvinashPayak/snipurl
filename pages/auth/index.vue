<template>
  <section class="h-screen grid place-content-center">
    <div class="container">
      <!-- Card -->
      <div class="card">
        <div class="flex justify-center">
          <div
            class="flex justify-center w-20 h-20 items-center rounded-full border shadow-xl border-white/20"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
              stroke-width="1.5"
              stroke="currentColor"
              class="w-8 h-8"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M16.5 10.5V6.75a4.5 4.5 0 1 0-9 0v3.75m-.75 11.25h10.5a2.25 2.25 0 0 0 2.25-2.25v-6.75a2.25 2.25 0 0 0-2.25-2.25H6.75a2.25 2.25 0 0 0-2.25 2.25v6.75a2.25 2.25 0 0 0 2.25 2.25Z"
              />
            </svg>
          </div>
        </div>

        <button
          @click="handleGithubLogin"
          class="btn btn-primary py-3 w-full mt-5"
        >
          Continue with Github!
        </button>

        <hr class="border-white/10 my-8" />

        <form @submit.prevent="handleLogin">
          <div class="form-group">
            <label for="email">Email</label>
            <input
              v-model="form.email"
              type="email"
              name="email"
              id="email"
              placeholder="abc@xyz.com"
            />
          </div>
          <div class="form-group">
            <label for="password">Password</label>
            <input
              v-model="form.password"
              type="password"
              name="password"
              id="password"
            />
          </div>
          <button type="submit" class="btn btn-primary w-full py-3 mt-5">
            <template v-if="isLoggingIn">Login</template>
            <template v-else>Signup</template>
          </button>

          <div class="text-center mt-5">
            <button v-if="isLoggingIn">
              Don't have an account?
              <span class="text-purple-500" @click="toggleLogin">Signup</span>.
            </button>
            <button v-else>
              Already have an account?
              <span class="text-purple-500" @click="toggleLogin">Login</span>.
            </button>
          </div>

          <p class="text-red-500 text-center mt-5">{{ errors }}</p>
        </form>
      </div>
      <!-- ./ Card -->
    </div>
  </section>
</template>
<script lang="ts" setup>
const form = reactive({
  email: "",
  password: "",
});
const errors = ref<string>("");
const isLoggingIn = ref<boolean>(false);
const supabaseAuth = useSupabaseClient();

const handleGithubLogin = () => {
  supabaseAuth.auth.signInWithOAuth({
    provider: "github",
  });
};

const resetError = () => {
  errors.value = ""
}

const handleSignup = async () => {
  try {
    const { data, error } = await supabaseAuth.auth.signUp({
      email: form.email,
      password: form.password,
    });

    if (error) {
      errors.value = error.message;
      return;
    }
    resetError()

    useRouter().push("/dashboard")

  } catch (error) {
    errors.value = "Something went wrong";
  }
};

const handleLogin = async () => {
  if (!form.email || !form.password) {
    errors.value = "Please fill all the fields";
    return;
  }

  if (!isLoggingIn.value) {
    handleSignup();
    return;
  }

  try {
    const { data, error } = await supabaseAuth.auth.signInWithPassword({
      email: form.email,
      password: form.password,
    });

    if (error) {
      errors.value = error.message;
      return;
    }

    resetError()

    useRouter().push("/dashboard")

  } catch (error) {
    errors.value = "Something went wrong";
  }
};

const toggleLogin = () => {
  isLoggingIn.value = !isLoggingIn.value;
};


</script>
