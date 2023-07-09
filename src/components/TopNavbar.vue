<template>
<!--  TODO WORK ON RESPONSIVENESS -->
  <div class="navbar">
    <div class="velocity-container">
      <div class="navbar-row">
        <div class="navbar-logo">
          <img src="../assets/images/velocity-logo.svg" alt="Velocity logo"/>
          <span>velocity</span>
        </div>
        <div class="profile-notifications-container">
          <router-link to="/notifications"
                       :class="`notifications-icon ${new_notification ? 'alert-notification' : ''}`">
            <img src="../assets/images/menu-icons/icon-bell.svg" alt="Bell Icon">
          </router-link>
          <router-link to="/notifications"
                       :class="`notifications-icon ${new_message ? 'alert-notification' : ''}`">
            <img src="../assets/images/menu-icons/icon-envelope.svg" alt="Envelope Icon">
          </router-link>
          <router-link to="/notifications">
            <img src="../assets/images/profile/joan-wilkins.png" alt="Joan Wilkins Profile Image" class="profile-image">
          </router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const new_notification = true;
const new_message = true;
</script>

<style lang="scss" scoped>
.navbar {
  height: 80px;
  background: var(--white);
  border-bottom: 1px solid #E4E8F0;
}

.velocity-container {
  height: 100%;

  .navbar-row {
    height: 100%;
    display: flex;
    justify-content: space-between;
    align-items: center;

    .navbar-logo {
      display: flex;
      flex-direction: row;

      span {
        margin-left: 9px;
        font-size: 19px;
        font-style: normal;
        font-weight: 500;
        line-height: normal;
        letter-spacing: -0.475px;
        text-transform: lowercase;
      }
    }
  }

  .profile-notifications-container {
    width: 138px;
    display: flex;
    justify-content: space-between;

    .profile-image {
      border-radius: 50%;
    }

    .notifications-icon {
      position: relative;

      &.alert-notification {

        &:after {
          content: "";
          display: block;
          border-radius: 50%;
          transition: 0.4s ease-out;
          width: 15px;
          height: 15px;
          background: var(--blue);
          border: 3px solid var(--grey);
          position: absolute;
          top: -2px;
          right: -2px;
        }
      }
    }
  }
}

</style>