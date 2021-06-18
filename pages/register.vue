<template>
  <div>
    <h1 class="font-bold pt-6 px-5">Register</h1>
    <form @submit.prevent="register" class="mt-4 flex flex-col space-y-4 px-5">
      <div class="flex flex-col space-y-1">
        <label for="username" class="w-full font-bold">Username</label>
        <input
          type="text"
          id="username"
          class="w-full rounded border-2 p-3"
          v-model="username"
          placeholder="Username"
        />
      </div>
      <div class="flex flex-col space-y-1">
        <label for="email" class="w-full font-bold">Email</label>
        <input
          type="email"
          id="email"
          class="w-full rounded border-2 p-3"
          v-model="email"
          placeholder="Email"
        />
      </div>
      <div class="flex flex-col space-y-1">
        <label for="password" class="w-full font-bold">Password</label>
        <input
          type="password"
          id="password"
          class="w-full rounded border-2 p-3"
          v-model="password"
          placeholder="Password"
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
        Register
      </button>
    </form>
    <p class="text-center mt-4">
      Don’t have an account yet?
      <nuxt-link to="/login" class="text-persianrose">Login</nuxt-link>
    </p>
  </div>
</template>
<script>
export default {
  data() {
    return {
      username: "",
      password: "",
      email: "",
    };
  },
  methods: {
    async register() {
      const user = await this.$strapi.register({
        username: this.username,
        email: this.email,
        password: this.password,
      });
      if (user) {
        this.$router.push("/login");
      }
    },
  },
};
</script>