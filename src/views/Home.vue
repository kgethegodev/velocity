<template>
  <main v-if="!loading">
    <div :class="`velocity-container ${is_filtered ? 'is_filtered' : ''} flex flex-row justify-between`">
      <div class="content-container">
        <div class="w-full flex flex-row justify-between mb-8 items-center">
          <div>
            <h1>Vehicles Dashboard <span>1 192 Total</span></h1>
          </div>
          <div>
            <button class="velocity-btn" @click="ToggleFilter">
              {{ is_filtered ? 'Hide Filters' : 'Show Filters' }}
            </button>
          </div>
        </div>

        <div class="vehicles-table">
          <!--          TODO FIX THIS ACCORDING TO THE COMPONENT-->
          <div class="vehicles-heading-container flex flex-row">
            <p class="vehicles-heading w-2/12 text-center">Name and ID</p>
            <p class="vehicles-heading w-2/12">Vehicle Model</p>
            <p class="vehicles-heading w-2/12">Next service</p>
            <p class="vehicles-heading w-2/12">trips</p>
            <p class="vehicles-heading w-4/12">Energy used</p>
          </div>

          <VehicleInfo v-for="vehicle in this.filtered_vehicles" :vehicle="vehicle"/>

        </div>
      </div>

      <div class="filter-container">
        <div class="filter-block block w-full bg-white">
          <p class="filter-heading">filter</p>

          <div class="filter-input-block">
            <div class="flex flex-row justify-between">
              <label for="trips_taken">
                Trips taken
              </label>
              <span class="input-count">{{ trips_taken }}</span>
            </div>
            <input type="range" class="w-full" max="2000" id="trips_taken" :value="trips_taken"
                   @change="setTripsTaken($event)">
          </div>

          <div class="filter-input-block">
            <div class="flex flex-row justify-between">
              <label for="service_due">
                Service due
              </label>
              <span class="input-count">{{ service_due }} days</span>
            </div>
            <input type="range" class="w-full" id="service_due" :value="service_due"
                   @change="setServiceDue($event)" max="21">
          </div>

          <div class="filter-input-block">
            <div class="flex flex-row justify-between">
              <label for="trips_taken">
                Vehicle model
              </label>
            </div>
            <input type="text" class="w-full filter-text-input" @change="setVehicleModel($event)"
                   placeholder="Vehicle model">
          </div>

          <div class="filter-input-block">
            <div class="flex flex-row justify-between">
              <label for="trips_taken">
                Status
              </label>
            </div>
            <input type="text" class="w-full filter-text-input" placeholder="Status" @change="setStatus($event)">
          </div>

          <div class="filter-input-block">
            <div class="flex flex-row justify-between">
              <label for="trips_taken">
                Location
              </label>
            </div>
            <input type="text" class="w-full filter-text-input" placeholder="Location" @change="setLocation($event)">
          </div>

        </div>
      </div>
    </div>
  </main>
</template>
<!--TODO LOGIC FOR FILTER TRY MAKE A FUNCTION THAT CONSIDERS ALL THE FILTER INPUTS INSTEAD OF DOING IT ONE BY ONE-->
<script setup>
import {ref} from "vue";
import VehicleInfo from "../components/content/VehicleInfo.vue";

const is_filtered = ref(localStorage.getItem('is_filtered') === "true");

const ToggleFilter = () => {
  is_filtered.value = !is_filtered.value;
  localStorage.setItem("is_filtered", is_filtered.value);
}
</script>

<script>
export default {
  data() {
    return {
      loading: false,
      post: null,
      error: null,
      vehicles: [],
      filtered_vehicles: [],
      trips_taken: 0,
      service_due: 0,
      vehicle_model: '',
      status: '',
      location: '',
    }
  },
  methods: {
    async getAllVehicles() {
      this.loading = true;
      const response = await fetch("https://www.afrihost.com/resources/fedev/mid/");
      this.vehicles = await response.json();
      this.filtered_vehicles = this.vehicles['vehicles'];
      this.loading = false;
    },

    setTripsTaken(event) {
      this.trips_taken = event.target.value;
      this.filter();
    },

    setServiceDue(event) {
      this.service_due = event.target.value;
      this.filter();
    },

    setVehicleModel(event) {
      this.vehicle_model = event.target.value;
      this.filter();
    },

    setStatus(event) {
      this.status = event.target.value;
      this.filter();
    },

    setLocation(event) {
      this.location = event.target.value;
      this.filter();
    },

    filter() {
      if (this.trips_taken !== 0 || this.service_due !== 0 || this.vehicle_model !== '') {
        this.filtered_vehicles = [];

        if (this.trips_taken !== 0) {
          for (let i = 0; i < this.vehicles['vehicles'].length; i++) {
            if (this.vehicles['vehicles'][i].trips <= this.trips_taken) {
              this.filtered_vehicles.push(this.vehicles['vehicles'][i]);
            }
          }
        }
        if (this.service_due !== 0) {
          for (let i = 0; i < this.vehicles['vehicles'].length; i++) {
            const today = new Date();
            const service_date = new Date(this.vehicles['vehicles'][i].service_due);
            const diff_time = Math.abs(today - service_date);
            const diff_days = Math.ceil(diff_time / (1000 * 60 * 60 * 24));

            if (diff_days === this.service_due) {
              this.filtered_vehicles.push(this.vehicles['vehicles'][i]);
            }
          }
        }
        if (this.vehicle_model !== '') {
          for (let i = 0; i < this.vehicles['vehicles'].length; i++) {
            if (this.vehicles['vehicles'][i].model.toLowerCase().includes(this.vehicle_model.toLowerCase())) {
              this.filtered_vehicles.push(this.vehicles['vehicles'][i]);
            }
          }
        }
      }
    }
  }
  ,
  mounted() {
    this.getAllVehicles();
  }
  ,
}
</script>

<style lang="scss" scoped>

.content-container {
  width: 100%;
  transition: 0.4s ease-out;
}

.filter-container {
  width: 0;
  overflow: hidden;
  transition: 0.4s ease-out;

  .filter-block {
    padding: 30px;

    .filter-input-block {
      margin-bottom: 34px;

      .input-count {
        color: var(--secondary);
      }

      .filter-text-input {
        padding: 11px 32px 11px 16px;
        border-radius: 5px;
        border: 1px solid #E0E7FF;
      }

      &:last-child {
        margin-bottom: 0;
      }
    }
  }

  .filter-heading {
    color: var(--secondary);
    font-size: 13px;
    font-style: normal;
    font-weight: 400;
    line-height: normal;
    letter-spacing: 1.213px;
    text-transform: uppercase;
    margin-bottom: 26px;
  }
}

.is_filtered {
  .filter-container {
    width: calc(30% - 24px)
  }

  .content-container {
    width: 70%
  }
}

.vehicles-table {
  .vehicles-heading-container {
    padding: 0 25px;

    .vehicles-heading {
      color: var(--light);
      font-size: 12px;
      font-style: normal;
      font-weight: 500;
      line-height: normal;
      letter-spacing: 1.12px;
      text-transform: uppercase;
      margin-bottom: 12px;
    }
  }
}
</style>