<template>
  <div>
    <div class="p-2 d-flex flex-wrap justify-content-between">
      <CreateRevenue @newRevenue="revenue" style="width: 40%" />
      <SubmitTable :revenueList="revenueGroup" style="width: 58%" />
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import CreateRevenue from "@/views/CreateRevenue.vue";
import SubmitTable from "@/views/SubmittedForm.vue";
// import { BButton, BBadge } from "bootstrap-vue";

export default {
  name: "HomeView",
  components: {
    CreateRevenue,
    SubmitTable,
  },
  data() {
    return {
      revenueGroup: [],
    };
  },
  methods: {
    revenue(data) {
      console.log(data);
      this.revenueGroup = data;
    },
  },
};
</script>
