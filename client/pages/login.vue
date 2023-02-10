<template>
  <div class="cc_auth">
    <h2 class="title has-text-centered">Login</h2>

    <form method="post" @submit.prevent="submit">
      <!-- <Notification :message="error" v-if="error" /> -->

      <div class="mb-3 mt-3">
        <label for="email" class="form-label">Email:</label>
        <input
          type="email"
          class="form-control"
          id="email"
          placeholder="Enter email"
          name="email"
          v-model="email"
          required
        />
      </div>
      <div class="mb-3 mt-3">
        <label for="password" class="form-label">Password:</label>
        <input
          v-bind:type="[showPassword ? 'text' : 'password']"
          class="form-control"
          id="password"
          placeholder="Enter password"
          name="password"
          v-model="password"
          required
        />
        <input type="checkbox" @click="showPassword = !showPassword" /> Show
        password
      </div>
      <!-- <div class="form-check mb-3">
        <label class="form-check-label">
          <input class="form-check-input" type="checkbox" name="remember"> Remember me
        </label>
      </div> -->
      <b-button variant="primary" class="w-100" type="submit">Login</b-button>
    </form>
    <div class="d-flex align-items-center w-100 mt-2">
      <div class="divider"></div>
      <p class="m-0 m-2">or</p>
      <div class="divider"></div>
    </div>
    <div class="mt-2 d-flex align-items-center justify-content-between w-100">
      <p>
        Don't have an account?
        <NuxtLink to="/signup" class="text-primary">Sign up</NuxtLink>
      </p>
      <p>
        Forgot password?
        <NuxtLink to="/forgotPwd" class="text-primary">Reset it</NuxtLink>
      </p>
    </div>
  </div>
</template>

<script>
import { mapActions } from "vuex";
// import Notification from '~/components/Notification'

export default {
  // middleware: 'guest',
  // components: {
  //     Notification,
  // },

  data() {
    return {
      email: "",
      password: "",
      showPassword: false,
      error: null,
    };
  },

  computed: {
    buttonLabel() {
      return this.showPassword ? "Hide" : "Show";
    },
  },

  methods: {
    toggleShow() {
      this.showPassword = !this.showPassword;
    },
    ...mapActions({
      logIn: "auth/logIn",
    }),

    submit() {
      const credentials = {
        email: this.email,
        password: this.password,
      };
      this.logIn(credentials)
        .then(() => {
          this.$router.push("/profile");
        })
        .catch((err) => {
          console.log(err);
          this.error = err.response;
        });
    },
  },
};
</script>
