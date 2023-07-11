<template class="none">
  <aside :class="`${is_expanded ? 'is_expanded' : ''}`">
    <button class="menu-toggle" @click="ToggleMenu">
      <img src="../assets/images/menu-icons/union.svg" alt="Union Icon">
    </button>
    <Menu />
  </aside>
</template>

<script setup>
import {ref} from "vue";
import Menu from "./content/Menu.vue";

const is_expanded = ref(localStorage.getItem("is_expanded") === "true");

const ToggleMenu = () => {
  is_expanded.value = !is_expanded.value;
  localStorage.setItem("is_expanded", is_expanded.value);
}
</script>

<style lang="scss" scoped>
aside {
  position: fixed;
  align-items: flex-start;
  padding-top: 22.25px;
  display: flex;
  flex-direction: column;
  background: var(--white);
  color: var(--dark);
  width: var(--sidebar-width);
  overflow: hidden;
  min-height: 100vh;
  transition: 0.4s ease-out;

  &.is_expanded {
    width: var(--sidebar-width-expanded);
  }

  .menu-toggle {
    width: var(--sidebar-width);
    margin-bottom: 1rem;
  }

  .welcome-profile-container {
    transition: 0.4s ease-out;
    opacity: 0;
    margin-top: 63px;
    display: flex;
    flex-direction: row;
    width: var(--sidebar-width-expanded);

    .welcome-profile-image {
      width: var(--sidebar-width);
      text-align: center;
      align-self: center;

      img {
        border-radius: 5px;
      }
    }

    .welcome-profile-text {
      align-self: center;
      font-size: 15px;
      font-style: normal;
      font-weight: 400;

      p {
        margin-bottom: 0
      }

      p:first-child {
        color: var(--primary);
        line-height: normal;
      }

      p:last-child {
        color: var(--light);
        line-height: 22px;
      }
    }
  }

  @media (max-width: 768px) {
    position: fixed;
    z-index: 99;
  }

}
</style>