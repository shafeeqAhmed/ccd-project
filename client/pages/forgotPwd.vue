<template>
  <div class="mt-5 p-5">
    <h2 class="title has-text-centered">Reset password</h2>

    <form method="post" @submit.prevent="resetPassword">
      <!-- <Notification :message="error" v-if="error" /> -->
      <div class="mb-3 mt-3">
        <p>Lost your password? Please enter your email address. You will receive a link 
          to create a new password via email.
        </p>
        <label for="email" class="form-label">Email:</label>
        <input type="email" class="form-control" id="email" placeholder="Enter email" name="email" v-model="email"
          required>
      </div>
      <b-button variant="outline-primary" type="submit">Reset password</b-button>
    </form>
  </div>
</template>

<script>
// import Notification from '~/components/Notification'

export default {
  // middleware: 'guest',
  // components: {
  //     Notification,
  // },

  data() {
    return {
      email: '',
      error: null,
    }
  },

  methods: {
    async resetPassword() {
      try {
        await this.$axios.post('reset-password', {
          email: this.email
        })
        this.$router.push('/');
      } catch (e) {
        console.log(e)
      }
    },
  },
}
</script>
