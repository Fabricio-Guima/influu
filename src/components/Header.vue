<template>
  <header>
    <nav>
      <router-link to="/">
        <img src="@/assets/Logotipo.svg" alt="logo influu"
      /></router-link>

      <div class="area-menu">
        <router-link class="menu-link" to="/">Home</router-link>
        <router-link class="menu-link" to="/texto">Texto</router-link>
        <router-link class="menu-link" to="/cep">CEP</router-link>
      </div>
    </nav>
  </header>
</template>

<script>
export default {
  name: "Header"
};
</script>

<style>
nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

nav a.menu-link {
  color: #ffffff;
  opacity: 0.7;
}

nav a.menu-link + a.menu-link {
  padding-left: 20px;
}

nav a.router-link-exact-active {
  color: #ffb0d6;
}
</style>
