<template>
  <div class="mobile-menu bg-white w-full">
    <div class="flex flex-row justify-between items-center velocity-container align-middle h-full">
      <div>
        <button class="menu-toggle" @click="ToggleMenu">
          <img src="../assets/images/menu-icons/union.svg" alt="Union Icon">
        </button>
      </div>
      <div><p class="text-center"><strong>Service reminders</strong></p></div>
      <div>
        <div class="profile-notifications-container">
          <router-link to="/notifications"
                       :class="`notifications-icon ${new_notification ? 'alert-notification' : ''}`">
            <img src="../assets/images/menu-icons/icon-bell.svg" alt="Bell Icon">
          </router-link>
        </div>
      </div>
    </div>
  </div>

  <div :class="`menu-holder  ${is_expanded ? 'is_expanded' : ''} `">
    <div class="menu-container">
      <Menu/>
    </div>
  </div>
</template>

<script setup>
import {ref} from "vue";
import Menu from "./content/Menu.vue";

const new_notification = true;
const is_expanded = ref(localStorage.getItem("is_expanded") === "true");

const ToggleMenu = () => {
  if (!is_expanded.value){
    localStorage.setItem("is_filtered", false);
  }
  is_expanded.value = !is_expanded.value;
  localStorage.setItem("is_expanded", is_expanded.value);
}
</script>

<style lang="scss" scoped>
.mobile-menu {
  height: 51px;
  border-bottom: 1px solid #E4E8F0;
  top: 0;
  right: 0;
  position: fixed;
}

.menu-holder {
  height: calc(100vh - 51px);
  background: rgba(46, 56, 77, 0.50);
  position: fixed;
  top: 51px;
  left: 0;
  display: none;
  opacity: 0;
  transition: 0.4s ease-out;
  width: 100%;

  &.is_expanded {
    display: block;
    opacity: 1;

    .menu-button-text, .welcome-profile-container {
      opacity: 1 !important;
    }

  }
}

.notifications-icon {
  position: relative;

  &.alert-notification {

    &:after {
      content: "";
      display: block;
      border-radius: 50%;
      transition: 0.4s ease-out;
      width: 14px;
      height: 14px;
      background: var(--blue);
      border: 3px solid var(--grey);
      position: absolute;
      top: -2px;
      right: -2px;
    }
  }
}

.menu-container {
  height: calc(100vh - 51px);
  position: fixed;
  top: 51px;
  left: 0;
  background: var(--white);
  width: min(60%, 215px);
}
</style>