<template>
  <div>
    <div class="d-flex align-items-end">
      <div class="flex-grow-1 p-2">
        <h2>Posts</h2>
      </div>

      <div class="p-2">
        <button type="button">Create</button>
      </div>
    </div>

    <ul class="p-0"
      v-if="posts.length"
    >
      <li
        v-for="(post, index) of posts"
        v-bind:key="post.id"
      >
        <div class="d-flex align-items-end">
          <div class="p-2">
            <span>{{ index + 1 }}.</span>
          </div>
          
          <div class="p-2 flex-grow-1">
            <router-link
              v-bind:to="`/posts/${ post.id }`"
            >
              <span>{{ post.title }}</span>
            </router-link>
          </div>

          <div class="p-2">
            <button type="button"
              v-on:click="deletePost(post)"
            >
              <span>Delete</span>
            </button>
          </div>
        </div>

        <hr />
      </li>
    </ul>

    <div
      v-else-if="postsLoading"
    >
      <p class="text-center">Loading...</p>
    </div>

    <div
      v-else-if="postsLoadingError"
    >
      <p class="text-center">Error on posts getting!</p>
    </div>

    <div
      v-else-if="!posts.length"
    >
      <p class="text-center">Yot dont have posts yet!</p>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'

  export default {
    data: () => ({
      posts: [],
      postsLoading: false,
      postsLoadingError: false,
    }),

    async mounted() {
      this.postsLoadingError = false
      this.postsLoading = true

      try {
        const response = await axios.get('https://jsonplaceholder.typicode.com/posts')
        this.posts = response.data
      } catch(error) {
        this.postsLoadingError = true
      }

      this.postsLoading = false
    },

    methods: {
      async deletePost(post) {
        const response = await axios.delete(`https://jsonplaceholder.typicode.com/posts/${ post.id }`)
        this.posts = this.posts.filter(element => element.id !== post.id)
      }
    }
  }
</script>
