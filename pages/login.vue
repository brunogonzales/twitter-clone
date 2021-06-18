<template>
  <div>
    <h1 class="font-bold pt-6 px-5">Login</h1>
    <form @submit.prevent="login" class="mt-4 flex flex-col space-y-4 px-5">
      <div class="flex flex-col space-y-1">
        <label for="username" class="w-full font-bold">Username</label>
        <input
          type="text"
          id="username"
          class="w-full rounded border-2 p-3"
          v-model="username"
        />
      </div>
      <div class="flex flex-col space-y-1">
        <label for="password" class="w-full font-bold">Password</label>
        <input
          type="password"
          id="password"
          class="w-full rounded border-2 p-3"
          v-model="password"
        />
      </div>
      <button
        type="submit"
        class="
          w-full
          py-4
          text-center
          bg-persianrose
          font-bold
          text-white
          rounded
        "
      >
        Login
      </button>
    </form>
    <p class="text-center mt-4">
      Don’t have an account yet?
      <nuxt-link to="/register" class="text-persianrose">Register</nuxt-link>
    </p>
  </div>
</template>
<script>
export default {
  data() {
    return {
      username: "",
      password: "",
    };
  },
  methods: {
    async login() {
      const user = await this.$strapi.login({
        identifier: this.username,
        password: this.password,
      });
      if (user) {
        this.$router.push("/");
      }
    },
  },
};
</script>