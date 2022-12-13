<template>
      <div id="app">
        <link rel="preconnect" href="https://fonts.googleapis.com">
        <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
        <link href="https://fonts.googleapis.com/css2?family=Manrope:wght@200;800&family=Montserrat:wght@100&family=Russo+One&display=swap" rel="stylesheet">
        <div class="wrap d-flex flex-column min-vh-100">
          <Header />
          <main class="flex-fill">
            <router-view/>
          </main>
          <Footer />
        </div>
  </div>
</template>


<script>
// @ is an alias to /src
import Footer from '@/components/Footer.vue'
import Header from '@/components/Header.vue'
import Vue from "vue";

export default {
  components: {

  },

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
