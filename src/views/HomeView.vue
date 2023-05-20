<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />

    <div class="row">
      <b-button variant="danger"> Notifications</b-button>
      <b-badge variant="primary">304</b-badge>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
import { BButton, BBadge } from "bootstrap-vue";

export default {
  name: "HomeView",
  components: {
    HelloWorld,
    BButton,
    BBadge,
  },
};
</script>
