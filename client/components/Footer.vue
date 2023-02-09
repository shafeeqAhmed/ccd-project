<template>
  <footer class="footer bg-dark text-white">
    <div>
      <p class="lead px-5"> {{ new Date().getFullYear() }} - Crypto Candle Data</p>
    </div>
    <div>
      <ul>
        <li>
          <a href="/terms-and-conditions"> Terms and Conditions </a>
        </li>
        <li>
          <a href="/privacy-policy"> Privacy Policy </a>
        </li>
      </ul>
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
