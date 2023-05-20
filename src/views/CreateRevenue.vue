<template>
  <div class="d-flex flex-wrap justify-content-center m-5 p-5">
    <div class="w-50 p-3" style="border: 1px solid grey; border-radius: 5px">
      <span class="h4 d-flex mb-5">Create Revenue Group</span>
      <div class="d-flex flex-wrap">
        <label class="">Group Name</label>
        <b-form-input class="w-100" />
      </div>
      <div class="d-flex flex-wrap mt-2">
        <label class="">Group Description</label>
        <div class="w-100" style="position: relative">
          <b-form-textarea
            v-model="revenueGroup.desc"
            maxLength="200"
            rows="6"
            class="w-100"
            @input="countChar"
          />
          <div style="position: absolute; right: 10px; bottom: 5px">
            {{ currDescChar }} / 200
          </div>
        </div>
      </div>
      <div class="d-flex flex-wrap mt-2 align-items-center">
        <input v-model="revenueGroup.special" type="checkbox" />
        <span style="margin-left: 10px">Special group</span>
      </div>
      <div class="w-100">
        <CreateRule />
      </div>
    </div>
  </div>
</template>
<style></style>
<script>
import { BFormInput, BFormTextarea } from "bootstrap-vue";
import CreateRule from "@/views/Components/CreateRule.vue";

export default {
  components: {
    BFormInput,
    BFormTextarea,
    CreateRule,
  },

  data() {
    return {
      revenueGroup: {
        name: "",
        desc: "",
        special: false,
      },
      currDescChar: 0,
    };
  },

  methods: {
    countChar() {
      this.currDescChar = this.revenueGroup.desc.length;
    },
  },
};
</script>
