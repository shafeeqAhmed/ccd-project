<template>
  <div class="mt-5 p-5">
    <div v-if="validJWT == true">
      <b-alert show variant="success">Email verification successful!</b-alert>

      <NuxtLink to="/login" class="btn btn-outline-primary"
        >Go to Log in</NuxtLink
      >
    </div>
    <div v-else-if="validJWT == false">
      <b-alert show variant="danger">
        Email verification not successful. The confirmation link is invalid or
        has expired.
      </b-alert>
      <NuxtLink to="/" class="btn btn-outline-primary">Go to Homepage</NuxtLink>
    </div>
  </div>
</template>

<script>
export default {
  // middleware: 'guest',

  data() {
    return {
      emailVerificationJWT: "",
      validJWT: null,
    };
  },

  mounted() {
    this.emailVerificationJWT = this.$route.query.token;
    this.verifyEmail();
  },

  methods: {
    async verifyEmail() {
      try {
        const res = await this.$axios.post("verify-email", {
          emailVerificationJWT: this.emailVerificationJWT,
        });
        this.validJWT = res.data;
      } catch (err) {
        console.log(err);
      }
    },
  },
};
</script>
