<template>
  <nav class="navbar navbar-expand-lg bg-dark navbar-dark py-3 fixed-top">
    <!-- TODO. <a href="#" class="navbar-brand">Logo here</a> -->
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navmenu">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="px-5 navbar-item has-dropdown is-hoverable collapse navbar-collapse" id="navmenu">
      <ul class="navbar-nav ms-auto">
        <li class="nav-item">
          <a href="/" class="nav-link">Home</a>
        </li>
        <!-- <li class="nav-item">
          <a href="/news" class="nav-link">News</a>
        </li> -->
        <li class="nav-item">
          <a href="/pricing" class="nav-link">Pricing</a>
        </li>
        <li class="nav-item">
          <a href="https://documenter.getpostman.com/view/11410028/TVCY5BQc" class="nav-link" target="_blank">API
            Docs</a>
        </li>
        <li class="nav-item">
          <a href="/candles" class="nav-link">Get Candles</a>
        </li>
        <li v-if="user" class="nav-item dropdown">
          <button class="btn btn-outline-primary dropdown-toggle" type="button" data-bs-toggle="dropdown" aria-expanded="false">
            {{ user.username }}
          </button>
          <ul class="dropdown-menu">
            <li>
              <a class="dropdown-item text-decoration-none" href="/profile">My Profile</a>
              <button class="dropdown-item btn btn-primary" @click="logout">Logout</button>
            </li>
          </ul>
        </li>
        <li v-else class="nav-item">
          <a href="/login" class="nav-link">Login</a>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'

export default {
  data() {
    return {
      isMenuOpen: false,
    }
  },
  computed: {
    ...mapGetters({
      authenticated: 'auth/authenticated',
      user: 'auth/user'
    }),
  },
  methods: {
    ...mapActions ({
      logOut: 'auth/logOut',
    }),    

    async logout() {
      this.logOut()
    },
  },
}
</script>

