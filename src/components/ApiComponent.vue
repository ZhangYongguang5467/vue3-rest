<template>
  <div>
    <h1>Random User</h1>
    <div v-if="user">
      <p>Name: {{ user.name.first }} {{ user.name.last }}</p>
      <p>Email: {{ user.email }}</p>
      <img :src="user.picture.large" alt="User Picture" />
    </div>
    <button @click="fetchUser">Fetch New User</button>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      user: null,
    };
  },
  methods: {
    async fetchUser() {
      try {
        const response = await axios.get('https://randomuser.me/api/');
        this.user = response.data.results[0];
      } catch (error) {
        console.error('Error fetching user:', error);
      }
    },
  },
  mounted() {
    this.fetchUser();
  },
};
</script>