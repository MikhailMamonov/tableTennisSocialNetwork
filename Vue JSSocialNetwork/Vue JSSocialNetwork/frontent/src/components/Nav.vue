<template>
 <nav class="navbar navbar-expand navbar-dark bg-dark">
      <router-link to="/" class="navbar-brand">bezKoder</router-link>
      <div class="navbar-nav mr-auto">
        <li class="nav-item">
          <router-link to="/" class="nav-link">Home</router-link>
        </li>
        <li class="nav-item">
          <router-link to="/tutorials" class="nav-link">Friends</router-link>
        </li>
        <li class="nav-item">
          <router-link to="/add" class="nav-link">Messages</router-link>
        </li>
        <li class="nav-item">
          <router-link to="/users" class="nav-link">Users</router-link>
        </li>
        <li class="nav-item">
          <router-link to="/about" class="nav-link">About</router-link>
        </li>
        <li class="nav-item">
          <router-link to="/register"  class="navbar-item" v-show="!isAuthenticated">Email signup</router-link>
        </li>
        <li class="nav-item">
          <router-link to="/login" class="nav-link" v-show="!isAuthenticated">Login</router-link>
        </li>
        <li class="nav-item"> 
          <a class="navbar-item" href="javascript:void(0)" v-on:click="logoff" v-show="isAuthenticated">Logoff {{profile.firstName}}</a>
        </li>
      </div>
    </nav>
</template>

<script>
import { EventBus } from '.././event-bus';
import { mapGetters } from 'vuex';

export default {
    name:'Nav',
  methods:{ 
      logoff() {
     this.$store.dispatch('auth/authLogout').then(() => {
        this.$router.push('/');
     });
  }
  },
  computed: mapGetters({
    isAuthenticated: 'auth/isAuthenticated',
    profile: 'user/profile',
  }),
   created() {
   EventBus.$on('logged-in', () => {
      // this doesn't currently do anything in this demo but does get fired on successful login.
      // leaving it here to show how to allow communication between unrelated components - ie. Store -> Component
      console.log('logged-in message received...');
    });
  },
  destroyed() {
    EventBus.$off('logged-in');
  }
}
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.router-link-exact-active {
  color: #209cee !important;
}
</style>
