<template>
  <div class="container">
    <div>
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
    (this as any).$axios.get('https://sample-app.getsandbox.com/users')
      .then((users: any) => {
        this.loading = false;
        this.users = users.data.data;
      });
  }
})
</script>

<style>
.user-list {
  margin-bottom: 10px;
}
</style>
