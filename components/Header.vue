<template>  
  <client-only>
  <nav class="uk-navbar-container" uk-navbar>
      <div class="uk-navbar-left">

          <ul class="uk-navbar-nav">
              <li class="uk-active"><router-link tag="a" class="navbar-brand" to="/" exact>Frontend test</router-link></li>
              <li v-if="username"><router-link tag="a" class="navbar-brand" to="/events" exact>Events</router-link></li>
              <li v-if="username"><router-link tag="a" class="navbar-brand" to="/events/register" exact>Register an Event</router-link></li>
          </ul>

      </div>

      <div class="uk-navbar-right">

          <ul class="uk-navbar-nav" v-if="username">
              <li><a href="#" class="uk-link-reset">{{ username }}</a></li>
              <li><a href="#" @click="logout">Logout</a></li>
          </ul>

          <ul class="uk-navbar-nav" v-else>
              <li><a href="/users/register">Signup</a></li>
              <li><a href="/users/signin">Signin</a></li>
          </ul>

      </div>

  </nav>
</client-only>

</template>

<script>  
import { mapMutations } from 'vuex'

export default {  
  computed: {
    // Set your username thanks to your getter
    username() {
      return this.$store.getters['auth/username']
    }
  },
  methods: {
    // Define your needed mutations, here: auth/logout
    ...mapMutations({
      logout: 'auth/logout'
    })
  }
}
</script> 