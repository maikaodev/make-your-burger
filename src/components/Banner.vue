<template>
  <div class="main-banner">
    <h1>Make your Burger</h1>
  </div>
</template>

<script>
export default {
  name: 'Banner'
}
</script>

<style scoped>
.main-banner {
  background-image: url(/img/bg-burger.jpg);
  background-repeat: no-repeat;
  background-position: 0 -250px;
  background-size: cover;

  height: 500px;

  display: flex;
  align-items: center;
  justify-content: start;
}
.main-banner h1 {
  background-color: #222;
  color: #fff;

  text-align: center;
  font-size: 60px;

  padding: 20px 40px;
}
</style>
