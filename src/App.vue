<template>
  <div id="app">
    <user />
  </div>
</template>

<script>
import User from "./components/User";

export default {
  name: "App",
  components: {
    User,
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
}

#app {
  height: 100vh;
  width: 100%;
  display: grid;
  place-content: center;
}
</style>
