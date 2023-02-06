<template>
  <footer class="px-5 pt-md-3 bg-dark text-white text-center fixed-bottom navbar">
    <div>
      <p class="lead px-5"> {{ new Date().getFullYear() }} - Crypto Candle Data</p>
    </div>
    <div>
      <p>
        <a href="/terms-and-conditions">
          Terms and Conditions
        </a>
      </p>
      <p>
        <a href="/privacy-policy">
          Privacy Policy
        </a>
      </p>
    </div>
    <div>
      <p>
        <a class="px-5 text-underline-hover" href="mailto: cryptocandledata@gmail.com">
          cryptocandledata@gmail.com
        </a> 
      </p>
    </div>
  </footer>
</template>

<script>
export default {

}
</script>

<style>
  a {
    color: inherit;
    text-decoration: none;
  }

  a:hover {
    color: inherit;
    text-decoration: underline;
  }
</style>