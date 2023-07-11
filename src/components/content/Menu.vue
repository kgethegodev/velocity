<template>

  <div class="welcome-profile-container">
    <div class="welcome-profile-image">
      <img src="../../assets/images/profile/joan-wilkins.png" alt="Joan Wilkins' Profile Image"/>
    </div>
    <div class="welcome-profile-text">
      <p>Welcome</p>
      <p>Joan Wilkins</p>
    </div>
  </div>

  <div class="menu">
    <router-link to="/" class="menu-button">
      <div class="menu-button-icon"><img src="../../assets/images/menu-icons/icon-dashboard.svg" alt="Dashboard icon"/>
      </div>
      <div class="menu-button-text">Overview</div>
    </router-link>
    <router-link to="/stats" class="menu-button">
      <div class="menu-button-icon"><img src="../../assets/images/menu-icons/icon-analytics.svg" alt="Dashboard icon"/>
      </div>
      <div class="menu-button-text">Stats</div>
    </router-link>
    <router-link to="/vehicles" class="menu-button">
      <div class="menu-button-icon"><img src="../../assets/images/menu-icons/icon-vehicles.svg" alt="Dashboard icon"/>
      </div>
      <div class="menu-button-text">Vehicles</div>
    </router-link>
    <router-link to="/config" class="menu-button">
      <div class="menu-button-icon"><img src="../../assets/images/menu-icons/icon-service.svg" alt="Dashboard icon"/>
      </div>
      <div class="menu-button-text">Config</div>
    </router-link>
    <router-link to="/map" class="menu-button">
      <div class="menu-button-icon"><img src="../../assets/images/menu-icons/icon-map.svg" alt="Dashboard icon"/></div>
      <div class="menu-button-text">Map</div>
    </router-link>
    <router-link to="/notifications" class="menu-button">
      <div class="menu-button-icon"><img src="../../assets/images/menu-icons/icon-chat.svg" alt="Dashboard icon"/></div>
      <div class="menu-button-text">Notifications</div>
    </router-link>
    <router-link to="/settings" class="menu-button">
      <div class="menu-button-icon"><img src="../../assets/images/menu-icons/icon-settings.svg" alt="Dashboard icon"/>
      </div>
      <div class="menu-button-text">Settings</div>
    </router-link>
  </div>
</template>

<style lang="scss" scoped>

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
      width: 0;
      background: var(--active-menu-item-border);
      position: absolute;
      top: 0;
      left: 0;
      opacity: 0;
      transition: 0.4s ease-out;
    }

    &.router-link-active, &:hover {
      background: var(--active-menu-item);

      &::before {
        opacity: 1;
        width: 3px;
      }
    }
  }
}

.is_expanded {
  .menu-button-text, .welcome-profile-container {
    opacity: 1 !important;
  }

}
</style>