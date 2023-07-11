<script setup>
import {ref} from "vue";

const is_expanded = ref(localStorage.getItem("is_expanded") === "true");

const ToggleMenu = () => {
  is_expanded.value = !is_expanded.value;
  localStorage.setItem("is_expanded", is_expanded.value);
}
</script>

<template>
  <button class="menu-toggle" @click="ToggleMenu">
    <img src="../assets/images/menu-icons/union.svg" alt="Union Icon">
  </button>
</template>

<style scoped lang="scss">

</style>