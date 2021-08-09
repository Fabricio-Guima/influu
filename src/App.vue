<template>
  <div id="app">
    <Header />
    <router-view class="view"></router-view>
  </div>
</template>

<script>
import Header from "@/components/Header";
export default {
  name: "App",
  components: {
    Header
  }
};
</script>
<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  text-decoration: none;
}
#app {
  padding: 40px;
  background-image: url("./assets/bg.svg"),
    linear-gradient(
      158deg,
      rgba(109, 27, 98, 1) 0%,
      rgba(139, 54, 128, 1) 35%,
      rgba(105, 48, 123, 1) 100%
    );

  max-width: 100%;
  height: 200vh;
  background-size: cover;
}

.view {
  height: 100vh;
}
</style>
