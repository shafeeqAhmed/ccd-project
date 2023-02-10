<template>
  <div class="auth_wrapper">
    <Navbar />
    <div class="cc_auth">
      <h2 class="title has-text-centered">Reset password</h2>

      <form method="post" @submit.prevent="resetPassword">
        <!-- <Notification :message="error" v-if="error" /> -->
        <div class="mb-3 mt-3">
          <p>
            Lost your password? Please enter your email address. You will
            receive a link to create a new password via email.
          </p>
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
        <b-button variant="primary" class="w-100" type="submit"
          >Reset password</b-button
        >
      </form>
      <div class="d-flex align-items-center w-100 mt-2">
        <div class="divider"></div>
        <p class="m-0 m-2">or</p>
        <div class="divider"></div>
      </div>
      <div class="mt-2 text-center">
        <p>
          <NuxtLink to="/login" class="text-primary">Login Here</NuxtLink>
        </p>
      </div>
    </div>
    <Footer />
  </div>
</template>

<script>
// import Notification from '~/components/Notification'

export default {
  // middleware: 'guest',
  // components: {
  //     Notification,
  // },
  layout: "authlayout",
  data() {
    return {
      email: "",
      error: null,
    };
  },

  methods: {
    async resetPassword() {
      try {
        await this.$axios.post("reset-password", {
          email: this.email,
        });
        this.$router.push("/");
      } catch (e) {
        console.log(e);
      }
    },
  },
};
</script>
