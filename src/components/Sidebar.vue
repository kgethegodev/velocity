<template>
  <aside :class="`${is_expanded ? 'is_expanded' : ''}`">
    <button class="menu-toggle" @click="ToggleMenu">
      <img src="../assets/images/menu-icons/union.svg" alt="Union Icon">
    </button>

    <div class="welcome-profile-container">
      <div class="welcome-profile-image">
        <img src="../assets/images/profile/joan-wilkins.png" alt="Joan Wilkins' Profile Image"/>
      </div>
      <div class="welcome-profile-text">
        <p>Welcome</p>
        <p>Joan Wilkins</p>
      </div>
    </div>

    <div class="menu">
      <!--    TODO TRANSFORM THE MENU ITEM INTO A COMPONENT-->
      <router-link to="/" class="menu-button">
        <div class="menu-button-icon"><img src="../assets/images/menu-icons/icon-dashboard.svg" alt="Dashboard icon"/>
        </div>
        <div class="menu-button-text">Overview</div>
      </router-link>
      <router-link to="/stats" class="menu-button">
        <div class="menu-button-icon"><img src="../assets/images/menu-icons/icon-analytics.svg" alt="Dashboard icon"/>
        </div>
        <div class="menu-button-text">Stats</div>
      </router-link>
      <router-link to="/vehicles" class="menu-button">
        <div class="menu-button-icon"><img src="../assets/images/menu-icons/icon-vehicles.svg" alt="Dashboard icon"/>
        </div>
        <div class="menu-button-text">Vehicles</div>
      </router-link>
      <router-link to="/config" class="menu-button">
        <div class="menu-button-icon"><img src="../assets/images/menu-icons/icon-service.svg" alt="Dashboard icon"/>
        </div>
        <div class="menu-button-text">Config</div>
      </router-link>
      <router-link to="/map" class="menu-button">
        <div class="menu-button-icon"><img src="../assets/images/menu-icons/icon-map.svg" alt="Dashboard icon"/></div>
        <div class="menu-button-text">Map</div>
      </router-link>
      <router-link to="/notifications" class="menu-button">
        <div class="menu-button-icon"><img src="../assets/images/menu-icons/icon-chat.svg" alt="Dashboard icon"/></div>
        <div class="menu-button-text">Notifications</div>
      </router-link>
      <router-link to="/settings" class="menu-button">
        <div class="menu-button-icon"><img src="../assets/images/menu-icons/icon-settings.svg" alt="Dashboard icon"/>
        </div>
        <div class="menu-button-text">Settings</div>
      </router-link>
    </div>
  </aside>
</template>

<script setup>
import {ref} from "vue";

const is_expanded = ref(localStorage.getItem("is_expanded") === "true");

const ToggleMenu = () => {
  is_expanded.value = !is_expanded.value;
  localStorage.setItem("is_expanded", is_expanded.value);
}
</script>

<style lang="scss" scoped>
//TODO CHECK WHY THERES MORE SPACE AT THE BOTTOM OF THE MENU ITEMS THAN AT THE TOP
aside {
  align-items: start;
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

    .menu-button-text, .welcome-profile-container {
      opacity: 1 !important;
    }
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

  .menu {
    margin-top: 31px;
    display: flex;
    flex-direction: column;

    .menu-button {
      transition: 0.2s ease-out;
      padding: 16px 0;
      display: flex;
      flex-direction: row;
      width: var(--sidebar-width-expanded);
      text-decoration: none;
      color: var(--secondary);
      position: relative;

      .menu-button-icon {
        width: var(--sidebar-width);
        text-align: center;
      }

      .menu-button-text {
        transition: 0.4s ease-out;
        align-self: center;
        font-style: normal;
        font-weight: 400;
        line-height: normal;
        opacity: 0;
      }

      &::before {
        content: "";
        height: 100%;
        width: 3px;
        background: var(--active-menu-item-border);
        position: absolute;
        top: 0;
        left: 0;
        opacity: 0;
        transition: 0.4s ease-out;
      }

      &.router-link-active, &:hover {
        background: var(--active-menu-item);
        //background: red;

        &::before {
          opacity: 1;
        }
      }
    }
  }

  @media (max-width: 768px) {
    position: fixed;
    z-index: 99;
  }

}
</style>