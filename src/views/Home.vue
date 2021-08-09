<template>
  <div class="home">
    <div class="content">
      <h1>Seja bem-vindo!</h1>
      <p class="sub-text">Selecione um teste abaixo</p>

      <div class="button-group">
        <router-link to="/texto" tag="button" class="btn"
          ><span>Texto</span></router-link
        >

        <router-link to="/cep" tag="button" class="btn"
          ><span>CEP</span></router-link
        >
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
// import Header from "@/components/Header";

export default {
  name: "Home",
  components: {}
};
</script>

<style scoped>
.home {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.content {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.content h1 {
  padding-bottom: 1rem;
  font-family: raleway;
  font-weight: bold;
  font-size: 36px;
  color: #ffffff;
}

.content p.sub-text {
  font-family: raleway;
  position: relative;
  margin-bottom: 94px;
  color: #ffffff;
}
.content p::after {
  content: "";
  display: block;
  max-width: 30px;
  height: 3px;
  margin: 24px auto 0 auto;
  background-color: #ef328d;
}

.button-group {
  display: flex;
  justify-content: space-between;
  width: 100%;
}

.button-group .btn {
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 4px;
  flex: 1;
  width: 47px !important;
  font-family: raleway;
  height: 21px;
  font-size: 18px;
  color: #ffffff;
  border: 1px solid #ffffff;
  padding: 20px 23px;
  background: transparent;
  cursor: pointer;
}

.button-group .btn + .btn {
  margin-left: 10px;
}
</style>
