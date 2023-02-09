<template>
  <div class="main-layout" ref="main_home">
    <Navbar />
    <div class="">
      <Nuxt />
    </div>
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
    },

  },
  mounted() {
    this.$refs['main_home'].classList.add('main-home')
    if(this.$route.name === 'index' ){
      this.$refs['main_home'].classList.add('main-home')
    }else{
      this.$refs['main_home'].classList.remove('main-home')
    }
  },
}
</script>

