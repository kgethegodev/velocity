<template>
  <div class="app">
    <Sidebar/>
    <div class="full-container">
      <TopNavbar/>
      <router-view/>
    </div>
  </div>
</template>

<script setup>
import Sidebar from "./components/Sidebar.vue";
import TopNavbar from "./components/TopNavbar.vue";
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

  main {
    flex: 1 1 0;
    padding: 2rem;

    @media (max-width: 768px) {
      padding-left: 6rem;
    }
  }

  .full-container{
    display: block;
    width: 100%;
  }
}

.velocity-container {
  width: min(1170px, 90%);
  margin: 0 auto;
}
</style>