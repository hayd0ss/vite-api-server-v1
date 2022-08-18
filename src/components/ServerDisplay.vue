<script>
import axios from 'axios';

export default {
  data () {
    return {
      welcomeMsg: "welcome viewer",
      posts: [],
      errors: [],
      userInfo: []
    }
  },

  // // Fetches posts when the component is created.
  // async created () {
  //   try {
  //     const response = await axios.get(`https://hk-netlify-apiv2.netlify.app/.netlify/functions/api`)
  //     this.posts = response.data
  //   } catch (e) {
  //     this.errors.push(e)
  //   }
  // },


  created () {
    this.getInfo();
  },

  methods: {
    getInfo () {
      axios.create({
        withCredentials: true
      });
      axios.get('https://hk-netlify-apiv2.netlify.app/.netlify/functions/api', { withCredentials: false, proxyHeaders: false, })
        .then(response => this.userInfo = response.data)
        .catch(error => this.userInfo = error.data);

    },
  }
}
</script>

<!-- Site build  -->
<template>

  <div>
    <h1>{{ welcomeMsg }}</h1>


    <table>
      <thead>
        <tr>
          <th></th>
          <th>ID</th>
          <th>Username</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(user, index) in userInfo" :key="user.id">
          <td>{{ index + 1 }}</td>
          <td>{{ user.ObjectId }}</td>
          <td>{{ user.userName }}</td>

          <td><img :src="user.imgUrl" :alt="user.alt" /></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped>
</style>
