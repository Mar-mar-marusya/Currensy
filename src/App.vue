<template>
  <div id="app" width="100%" heigth="100%">
    <!-- <img
      alt="Vue logo"
      src="./assets/PngItem_225184.png"
      id="Logo"
      class="smallMargin"
    /> -->
    <HelloWorld  />
    <Currensy currensy=""/>

  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import Currensy from "./components/Currensy.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
    Currensy,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background-image: url("./assets/background.jpg");
  background-repeat: repeat-y;
}
#Logo {
  width: 300px;
}
.smallMargin {
  margin: 1em;
}
</style>
