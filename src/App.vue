<script>
import Navigation from "./components/Navigation/Navigation.vue";
export default {
  name: "App",
  components: { Navigation },
};
</script>
<template>
  <div class="app">
    <Navigation />
    <router-view></router-view>
  </div>
</template>

<style lang="scss">
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: "Raleway", sans-serif;
  font-weight: 400;
}
.app {
  min-width: 100vh;
  position: relative;
  background-color: #f1f1f1;
}
.container {
  padding: 0 20px;
  max-width: 1140px;
  margin: 0 auto;
}
</style>
