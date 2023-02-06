<template>
  <div class="mt-5 p-5">
    <h2 class="title has-text-centered">Sign up</h2>

    <form method="post" @submit.prevent="submit">
      <!-- <Notification v-if="error" :message="error" /> -->

      <div class="mb-3 mt-3">
        <label for="username" class="form-label">Username:</label>
        <input type="username" class="form-control" id="username" placeholder="Enter username" name="username"
          v-model="username" required>
      </div>
      <div class="mb-3 mt-3">
        <label for="email" class="form-label">Email:</label>
        <input type="email" class="form-control" id="email" placeholder="Enter email" name="email" v-model="email"
          required>
      </div>
      <div class="mb-3 mt-3">
        <label for="password" class="form-label">Password:</label>
        <input v-bind:type="[showPassword ? 'text' : 'password']" class="form-control" id="password" placeholder="Enter password" name="password"
          v-model="password" required>
        <input type="checkbox" @click="showPassword = !showPassword"> Show password
      </div>
      <b-button variant="outline-primary" type="submit">Sign up</b-button>
    </form>
    <div class="mt-4 has-text-centered">
      <p>
        Already got an account?
        <a class="text-primary" href="/login">Login</a>
      </p>
    </div>
  </div>
</template>

<script>
import { mapActions } from 'vuex'
// import Notification from '~/components/Notification'

export default {
  // components: {
  //   Notification,
  // },
  // middleware: 'guest',
  data() {
    return {
      username: '',
      email: '',
      password: '',
      showPassword: false,
      error: null,
    }
  },
  
  computed: {
    buttonLabel() {
      return (this.showPassword) ? "Hide" : "Show";
    }
  },

  methods: {
    toggleShow() {
      this.showPassword = !this.showPassword;
    },

    ...mapActions ({
      signUp: 'auth/signUp',
    }),

    submit() {
      const credentials = {
        username: this.username,
        email: this.email,
        password: this.password
      }
      this.signUp(credentials).then(() => {
        this.$router.push('/pendingEmailVerification')
      
      }).catch((err) => {
        console.log(err)
        this.error = err.response        
      });
    },
  },
}
</script>
