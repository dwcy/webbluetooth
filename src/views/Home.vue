<template>
  <div class="home">
      <img class="logo"  src="http://www.queenslab.se/wp-content/themes/Queens/assets/img/menu-icon.svg" alt="">
    <Bluetooth />
  </div>
</template>

<script>

import Bluetooth from "@/components/Bluetooth.vue";

export default {
  name: "home",
  components: {
    Bluetooth
  }
};
</script>

<style>
.logo {

   height: 100px;
   background-color: rgb(57, 201, 57);

}
</style>