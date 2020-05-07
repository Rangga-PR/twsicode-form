<template>
  <div id="app">
    <twis-form />
  </div>
</template>

<script>
  import TwisForm from "./components/twisform/TwisForm";
  export default {
    name: "App",
    components: {
      TwisForm,
    },
  };
</script>

<style lang="scss">
  @charset "utf-8";
  @import url("https://fonts.googleapis.com/css2?family=Montserrat&display=swap");
  @import url("https://fonts.googleapis.com/icon?family=Material+Icons");

  #app {
    overflow: auto;
    display: flex;
    justify-content: center;
    align-items: center;
    height: fit-content;
    padding: 5vh 0;
    background-image: url("./assets/img/bg-dusk.webp");
    font-family: "Montserrat", sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  @media only screen and (min-width: 768px) {
    #app {
      height: 100vh;
      padding: 0;
    }
  }

  body {
    margin: 0;
  }
</style>
