<template>
  <Navbar :logo="logo_src" :alt="app_name" />
  <router-view />
  <Footer />
</template>

<script>
import Navbar from './components/Navbar.vue'
import Footer from './components/Footer.vue'

export default {
  components: {
    Navbar,
    Footer
  },
  data() {
    return {
      logo_src: './img/logo.png',
      app_name: 'Make your burguer'
    }
  }
}
</script>
<style>
* {
  font-family: Helvetica;
  padding: 0px;
  margin: 0px;
  box-sizing: border-box;
}

.main-container {
  margin: 48px;
  min-height: 250px;
}
h1 {
  text-align: center;
  font-size: 40px;
  margin-bottom: 32px;
  color: #222;
}
</style>
