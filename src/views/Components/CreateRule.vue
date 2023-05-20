<template>
  <div class="">
    <span class="rule-title">Rules</span>
    <div class="d-flex justify-content-end align-items-center">
      <b-badge class="text-primary" style="background: #00f0ff1a">
        <feather-icon icon="PlusIcon" style="" /> Add
      </b-badge>
    </div>
    <div class="mt-2 p-2" style="border: 1px dashed grey; border-radius: 5px">
      <span class="rule-sub">sds</span>
    </div>
  </div>
</template>
<style scoped>
.rule-title {
  font-size: 20px;
}
.rule-sub {
  font-size: 18px;
}
</style>
<script>
import { BBadge } from "bootstrap-vue";
// import CreateRule from "@/views/Components/CreateRule.vue";

export default {
  components: {
    BBadge,
  },

  data() {
    return {
      rule: [
        {
          name: "",
          field: "",
          operator: "",
          parameter: [],
          amountRev: "",
        },
      ],
      fieldList: [],
      operatorList: [],
    };
  },

  methods: {
    countChar() {
      this.currDescChar = this.revenueGroup.desc.length;
    },
  },
};
</script>
