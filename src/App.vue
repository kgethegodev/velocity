<template>
  <div class="app">
    <Sidebar v-if="!isMobile()"/>
    <MobileMenu v-else/>
    <div class="full-container">
      <TopNavbar v-if="!isMobile()"/>
      <router-view/>
    </div>
  </div>
</template>

<script setup>
import Sidebar from "./components/Sidebar.vue";
import TopNavbar from "./components/TopNavbar.vue";
import MobileMenu from "./components/MobileMenu.vue";

function isMobile() {
  return screen.width <= 768;
}
</script>

<style lang="scss">
:root {
  --primary: #2E384D;
  --secondary: #8798AD;
  --grey: #F4F6FC;
  --dark: #2E384D;
  --light: #BFC5D2;
  --blue: #2E5BFF;
  --white: #FFFFFF;
  --active-menu-item: #2E5BFF1A;
  --active-menu-item-border: #2E5BFF;
  --sidebar-width: 80px;
  --sidebar-width-expanded: 215px;
  --body-font-size: 15px;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Rubik', sans-serif;
}

body {
  color: var(--primary);
  background: var(--grey);
  font-size: var(--body-font-size);
}

button {
  cursor: pointer;
  appearance: none;
  border: none;
  outline: none;
  background: none;
}

.app {
  display: flex;
  @media (max-width: 768px) {
    display: block;
    padding-top: 81px;
  }

  main {
    margin-top: 62px;
    @media (max-width: 768px) {
      margin-top: 30px;
    }
  }

  .full-container {
    display: block;
    width: 100%;
  }
}

.velocity-container {
  width: min(1170px, calc(100% - 50px));
  margin: 0 auto;
}

h1 {
  font-size: 28px;
  font-style: normal;
  font-weight: 300;
  line-height: 32px;

  span {
    color: var(--secondary);
    font-size: 15px;
    font-style: normal;
    font-weight: 400;
    line-height: 22px;
  }
}

.velocity-btn {
  color: var(--white);
  text-align: center;
  padding: 10px 0;
  width: 200px;
  background: var(--blue);
  border-radius: 5px;

  @media (max-width: 768px){
    width: 100%;
  }
}
</style>