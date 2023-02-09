<template>
  <nav class="header navbar navbar-expand-lg bg-dark navbar-dark">
    <div class="container">
      <!-- TODO. <a href="#" class="navbar-brand">Logo here</a> -->
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navmenu">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="sidebar-overlay has-dropdown is-hoverable collapse navbar-collapse" id="navmenu"
        data-bs-toggle="collapse" data-bs-target="#navmenu"></div>
      <div class="px-5 navbar-item has-dropdown is-hoverable collapse navbar-collapse" id="navmenu">
        <ul class="navbar-nav ms-auto">
          <li class="nav-item">
            <NuxtLink to="/"  class="nav-link"> Home </NuxtLink>
          </li>
          <!-- <li class="nav-item">
            <a href="/news" class="nav-link">News</a>
          </li> -->
          <li class="nav-item">
            <NuxtLink to="/pricing"  class="nav-link"> Pricing </NuxtLink>
          </li>
          <li class="nav-item">
            <a href="https://documenter.getpostman.com/view/11410028/TVCY5BQc" class="nav-link" target="_blank">API
              Docs</a>
          </li>
          <li class="nav-item">
            <NuxtLink to="/candles"  class="nav-link"> Get Candles </NuxtLink>
          </li>
          <li v-if="user" class="nav-item dropdown">
            <button class="btn btn-outline-primary dropdown-toggle" type="button" data-bs-toggle="dropdown"
              aria-expanded="false">
              {{ user.username }}
            </button>
            <ul class="dropdown-menu">
              <li>
                <NuxtLink to="/profile" class="dropdown-item text-decoration-none"> My Profile </NuxtLink>
                <button class="dropdown-item btn btn-primary" @click="logout">
                  Logout
                </button>
              </li>
            </ul>
          </li>
          <li v-else class="nav-item">
            <a href="/login" class="nav-link">Login</a>
            <!-- <NuxtLink to="/login">Login</NuxtLink> -->
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
import { mapActions, mapGetters } from "vuex";

export default {
  data() {
    return {
      isMenuOpen: false,
      isActive: false,
    };
  },
  computed: {
    ...mapGetters({
      authenticated: "auth/authenticated",
      user: "auth/user",
    }),
  },
  methods: {
    ...mapActions({
      logOut: "auth/logOut",
    }),

    async logout() {
      this.logOut();
    },
  },

};
</script>

<style scopped>
@media (max-width: 1000px) {
  .sidebar-overlay {
    position: fixed;
    width: 100%;
    height: 100%;
    left: 0;
    top: 0;
    background: #000;
    opacity: 0;
    z-index: 1050;
  }

  .navbar .navbar-toggler {
    z-index: 1060;
    position: relative;
  }

  .navbar .navbar-item {
    position: relative;
    z-index: 1060;
  }
}
</style>
