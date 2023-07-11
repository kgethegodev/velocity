<template>
  <div class="vehicle-info-row bg-white flex flex-row justify-between w-full items-center">
    <div class="flex flex-row profile-col items-center">
      <img :src="getImageUrl(props.vehicle.id)"
           :alt="`${props.vehicle.name}'s profile picture`"
           class="mw-auto d-block mr-2">
      <div>
        <p>{{ props.vehicle.name }}</p>
        <p>#{{ props.vehicle.id }}</p>
      </div>
    </div>
    <div class="profile-col lg:block md:block hidden">
      <p>{{ props.vehicle.model }}</p>
    </div>
    <div class="profile-col">
      <p>{{ props.vehicle.service_due }}</p>
    </div>
    <div class="profile-col lg:block md:block hidden">
      <p>{{ props.vehicle.trips }}</p>
    </div>
    <div class="profile-col lg:block md:block hidden">
      <p>{{ props.vehicle.energy_usage }} kWh</p>
    </div>
    <div class="profile-col text-right">
      <router-link to="" class="profile-link">Manage</router-link>
    </div>
  </div>
</template>

<script setup>
const props = defineProps(['vehicle']);

function getImageUrl(name) {
  return new URL(`../../assets/images/profile/users/${name}.png`, import.meta.url).href
}
</script>

<style lang="scss" scoped>
.vehicle-info-row {
  padding: 20px 25px;
  border-radius: 1px;
  border: 1px solid rgba(46, 91, 255, 0.08);
  margin-bottom: 10px;

  .profile-col {
    width: calc((100% / 6) - 10px);

    div {
      p:first-child {
        font-weight: 500;
      }

      p:last-child {
        color: var(--secondary);
      }
    }

    .profile-link {
      color: var(--blue);
      font-weight: 500;
    }

    img {
      width: 34px;
      height: 34px;
    }

    @media (max-width: 768px) {
      width: calc(100% / 3);
    }
  }

  @media (max-width: 768px) {
    padding: 20px 12px
  }
}
</style>