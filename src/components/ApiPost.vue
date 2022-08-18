<template>
  <div>
    <input type="text" v-model="postBody" @change="postPost()" />
    <ul v-if="errors && errors.length">
      <li v-for="error of errors">
        {{ error.message }}
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data () {
    return {
      postBody: '',
      errors: []
    }
  },

  methods: {
    // Pushes posts to the server when called.
    async postPost () {
      try {
        await axios.post(`'https://hk-netlify-apiv2.netlify.app/.netlify/functions/api`, {
          withCredentials: true,
          proxyHeaders: false,
          body: this.postBody
        })
      } catch (e) {
        this.errors.push(e)
      }
    }
  }
}
</script>