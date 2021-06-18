<template>
  <main>
    <header class="px-5 py-4 flex">
      <div v-if="$strapi.user" class="flex w-full">
        <p>{{ $strapi.user.username }}</p>
        <p class="ml-auto" @click="logout">Logout</p>
      </div>
      <nuxt-link v-else to="/login" class="ml-auto">Login</nuxt-link>
    </header>
    <form class="pt-6 px-5 flex space-x-1" @submit.prevent="submitPost">
      <input
        class="pl-2 py-3 border-2 rounded w-1/2"
        type="text"
        v-model="post"
        placeholder="Type something..."
      />
      <button
        class="rounded bg-persianrose py-4 w-1/2 font-bold text-white"
        type="submit"
      >
        Post
      </button>
    </form>
    <section class="px-5 mt-5 flex flex-col space-y-5">
      <div v-for="post in posts" :key="post.id" class="flex space-x-2">
        <div
          class="
            rounded-full
            w-9
            h-9
            bg-gray-200
            flex
            items-center
            justify-center
          "
        >
          <span v-if="post.author" class="capitalize">{{
            post.author.username[0]
          }}</span>
          <span v-else>?</span>
        </div>
        <p class="pt-1">{{ post.content }}</p>
      </div>
    </section>
  </main>
</template>
<script>
export default {
  async asyncData({ $strapi }) {
    const posts = await $strapi.find("posts");
    return {
      posts,
    };
  },
  data() {
    return {
      post: "",
    };
  },
  methods: {
    async submitPost() {
      const savedPost = await this.$strapi.create("posts", {
        content: this.post,
        author: this.$strapi.user,
      });
      this.posts.push(savedPost);
      this.post = "";
    },
    logout() {
      this.$strapi.logout();
      this.$router.push("/login");
    },
  },
};
</script>
