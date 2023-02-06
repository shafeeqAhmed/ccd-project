<template>
  <div class="mt-5 p-5">
    <h2 class="title has-text-centered">Login</h2>

    <form method="post" @submit.prevent="submit">
      <!-- <Notification :message="error" v-if="error" /> -->

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
      <!-- <div class="form-check mb-3">
        <label class="form-check-label">
          <input class="form-check-input" type="checkbox" name="remember"> Remember me
        </label>
      </div> -->
      <b-button variant="outline-primary" type="submit">Login</b-button>
    </form>
    <div class="mt-4 has-text-centered">
      <p>
        Forgot password?
        <a class="text-primary" href="/forgotPwd">Reset it</a>
      </p>
    </div>
    <div class="mt-4 has-text-centered">
      <p>
        Don't have an account?
        <a class="text-primary" href="/signup">Sign up</a>
      </p>
    </div>
  </div>
</template>

<script>
import { mapActions } from 'vuex'
// import Notification from '~/components/Notification'

export default {
  // middleware: 'guest',
  // components: {
  //     Notification,
  // },

  data() {
    return {
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
      logIn: 'auth/logIn',
    }),

    submit() {
      const credentials = {
        email: this.email,
        password: this.password
      }
      this.logIn(credentials).then(() => {
        this.$router.push('/')
      
      }).catch((err) => {
        console.log(err)
        this.error = err.response        
      });
    },
  },
}
</script>
