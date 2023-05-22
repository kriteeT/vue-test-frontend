<template>
  <div id="app">
    <div class="container mt-4 mx-auto">
      <div
        v-if="posts"
        class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4"
      >
        <div
          v-for="post in posts"
          :key="post.id"
          :title="post.title"
          @click="handleClick(post.id)"
          class="
            card
            m-2
            cursor-pointer
            border border-gray-400
            rounded-lg
            hover:shadow-md hover:border-opacity-0
            transform
            hover:-translate-y-1
            transition-all
            duration-200
          "
        >
          <div class="m-3">
            <h2 class="text-lg mb-2">
              {{ post.title }}
              <span
                class="
                  text-sm text-teal-800
                  font-mono
                  bg-teal-100
                  inline
                  rounded-full
                  px-2
                  align-top
                  float-right
                  animate-pulse
                "
                >Tag</span
              >
            </h2>
            <p
              class="
                font-light font-mono
                text-sm text-gray-700
                hover:text-gray-900
                transition-all
                duration-200
              "
            >
              {{ post.body }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Home',
  components: {
    // HelloWorld,
  },
  data() {
    return {
      posts: null,
    };
  },
  async created() {
    const response = await fetch('https://jsonplaceholder.typicode.com/posts');
    const resJson = await response.json();
    this.posts = resJson;
  },
  methods: {
    handleClick(postId) {
      this.$router.push({ name: 'post', params: { id: postId } });
    },
  },
};
</script>
