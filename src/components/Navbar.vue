<template>
  <div id="nav">
    <router-link to="/" id="logo_url">
      <img :src="logo" :alt="alt" id="logo" />
    </router-link>
    <router-link to="/">Home</router-link>
    <router-link to="/pedidos">Pedidos</router-link>
  </div>
</template>

<script>
export default {
  name: 'Navbar',
  props: ['logo', 'alt']
}
</script>

<style scoped>
#nav {
  background-color: #222;
  border-bottom: 4px solid #111;

  padding: 16px 48px;

  display: flex;
  justify-content: flex-end;
  align-items: center;
}

#nav #logo_url {
  margin: auto;
  margin-left: 0px;
}

#logo {
  width: 40px;
  height: 40px;
}

#nav a {
  color: #fcba03;
  text-decoration: none;

  margin: 16px;

  transition: 0.5s;
}

#nav a:hover {
  color: #fff;
}
</style>
