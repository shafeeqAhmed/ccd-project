<template>
  <div>
    <Navbar />
    <Nuxt />
    <Footer />
  </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'

export default {
  data() {
    return {}
  },

 computed: {
    ...mapGetters({
      authenticated: 'auth/authenticated',
      user: 'auth/user'
    }),    
 },

  mounted() {
    this.keepUserLoggedIn()
  },

  methods: {
    ...mapActions({
      attempt: 'auth/attempt',
    }),

    async keepUserLoggedIn() {
      await this.attempt(localStorage.getItem('USER_TOKEN'))
      console.log('default - ', this.user)
    }
  }
}
</script>

