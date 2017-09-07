<template>
  <section class="container">
    <img src="~assets/img/logo.png" alt="Nuxt.js Logo" class="logo" />
    <h1 class="title">
      USERS
    </h1>

    <ul class="users">
      <li v-for="(user, index) in users" :key="index" class="user">
        <nuxt-link :to="{ name: 'id', params: { id: index }}">
          {{ user.name }}
        </nuxt-link>
      </li>
    </ul>
  </section>
</template>

<script lang="ts">
import axios from '~/plugins/axios'; 
import { Component, Inject, Model, Prop, Vue, Watch } from 'nuxt-property-decorator'

@Component({})
export default class UserList extends Vue {
  users: Array<IUser> = [];

  async asyncData ({ params }) {
    var res = await axios.get('/api/users');
    console.log(params);
    return {
      users: res.data
    }
  }

  head () {
    return {
      title: 'Users'
    }
  }
}
</script>

<style scoped>
.title
{
  margin: 30px 0;
}
.users
{
  list-style: none;
  margin: 0;
  padding: 0;
}
.user
{
  margin: 10px 0;
}
</style>
