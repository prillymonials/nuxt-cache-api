<template>
  <div class="container">
    <div>
      <button @click="handleAddUser" v-if="!loading">
        Add User
      </button>
      <div v-if="loading">Loading</div>
      <div
        v-else
        class="user-list"
        v-for="user in users"
        :key="`user-${user.id}`"
      >
        <ul>
          <li>{{user.id}}</li>
          <li>{{user.name}}</li>
          <li>{{user.username}}</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  data() {
    return {
      loading: true,
      users: [],
    };
  },
  mounted() {
    this.getUserList();
  },
  methods: {
    async handleAddUser() {
      this.loading = true;
      const id = Math.floor(Math.random() * 10000) + 1;
      await (this as any).$axios.post('https://sample-app.getsandbox.com/users', {
        id,
        name: 'Random',
        username: `randomuser${id}`
      });
      this.getUserList();
    },
    getUserList() {
      (this as any).$axios.get('https://sample-app.getsandbox.com/users')
        .then((users: any) => {
          this.loading = false;
          this.users = users.data.data;
        });
    }
  }
})
</script>

<style>
.user-list {
  margin-bottom: 10px;
}
</style>
