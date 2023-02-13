<template>
  <div class="auth_wrapper profile">
    <Navbar />
    <div class="mt-5 p-5 w-100">
      <h2 class="display-4 text-center">My Profile</h2>
      <b-container class="py-5 bv-example-row">
        <b-row>
          <b-col class="navbar-nav text-center">
            <b-link v-on:click="displayHidden('account')" class="nav-item">Account details</b-link>
            <b-link v-on:click="displayHidden('subscription')" class="nav-item">My Subscription</b-link>
            <b-link v-on:click="displayHidden('apiKeys')" class="nav-item">API Key</b-link>
          </b-col>
          <b-col class="text-center" style="border-left: 1px solid #ccc;">
            <div v-if="account || placeholder">
              <p>
                <strong>Username:</strong>
                {{ user.username }}
              </p>
              <p>
                <strong>Email:</strong>
                {{ user.email }}
              </p>
            </div>
            <div v-else-if="subscription">
              <strong>Plan:</strong>
              {{ user.plan }}<br/>
              <a class="my-3 btn btn-primary" href="/pricing">Change plan</a>
            </div>
            <div v-else-if="apiKeys">
              <strong>API Key:</strong>
              {{ user.apiKey }}<br/>
              <b-button class="my-3" variant="outline-primary" @click="generateAPIKey()">Generate new API Key</b-button>
              <p class="small">This will immediately revoke your current API key and display a new one here for you to copy.</p>
            </div>
          </b-col>
        </b-row>
      </b-container>
    </div>
    <Footer />
  </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'

export default {
    // middleware: 'auth',
    layout: "authlayout",
  data() {
    return {
      account: false,
      subscription: false,
      apiKeys: false,
      placeholder: true
    }
  },
  computed: {
    ...mapGetters({
      authenticated: 'auth/authenticated',
      user: 'auth/user'
    }),
  },

  methods: {
    ...mapActions({
      attempt: 'auth/attempt',
    }),

    async generateAPIKey() {
      await this.$axios.$get(`/generate-api-key?email=${this.user.email}`)
      await this.attempt(localStorage.getItem('USER_TOKEN'))
    },

    displayHidden(item) {
      this.placeholder = false

      if (item == 'account' && !this.account) {
        this.account = !this.account
        this.subscription = false
        this.apiKeys = false
      } else if (item == 'subscription' && !this.subscription) {
        this.account = false
        this.apiKeys = false
        this.subscription = !this.subscription
      } else if (item == 'apiKeys' && !this.apiKeys) {
        this.account = false
        this.subscription = false
        this.apiKeys = !this.apiKeys
      }
    },
  },
}
</script>
