<template>
  <main>
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
        <div class="rounded-full w-9 h-9 bg-gray-200"></div>
        <p class="pt-1">{{ post.content }}</p>
      </div>
    </section>
  </main>
</template>
<script>
export default {
  data() {
    return {
      post: "",
      posts: [{ content: "Hello there" }],
    };
  },
  methods: {
    submitPost() {
      this.posts.push({ content: this.post });
      this.post = "";
    },
  },
};
</script>
