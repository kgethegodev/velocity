<template>
  <div class="app">
    <Sidebar/>
    <router-view/>
  </div>
</template>

<script setup>
import Sidebar from "./components/Sidebar.vue";
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
}
</style>