<template>
  <div class="d-flex flex-wrap p-1">
    <div
      class="p-3 w-100"
      style="border: 1px solid lightgray; border-radius: 5px"
    >
      <span class="h4 d-flex mb-5">Create Revenue Group</span>
      <div class="d-flex flex-wrap">
        <label class="">Group Name</label>
        <b-form-input
          v-model="revenueGroup.name"
          placeholder="Name"
          class="w-100"
        />
      </div>
      <div class="d-flex flex-wrap mt-2">
        <label class="">Group Description</label>
        <div class="w-100" style="position: relative">
          <b-form-textarea
            v-model="revenueGroup.desc"
            maxLength="200"
            rows="6"
            placeholder="Description"
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
      <div class="w-100 mt-4">
        <CreateRule :rules="revenueGroup.rule" />
      </div>
      <div class="w-100 mt-2 d-flex justify-content-end">
        <b-button
          variant="outline-secondary"
          style="color: #000"
          @click="resetForm"
          >Reset</b-button
        >
        <b-button @click="submitForm" class="ml-2" variant="primary"
          >Submit</b-button
        >
      </div>
    </div>
  </div>
</template>
<style></style>
<script>
import { BFormInput, BFormTextarea, BButton } from "bootstrap-vue";
import CreateRule from "@/views/Components/CreateRule.vue";

export default {
  components: {
    BFormInput,
    BFormTextarea,
    BButton,
    CreateRule,
  },

  data() {
    return {
      revenueGroup: {
        name: "",
        desc: "",
        special: false,
        rule: [
          {
            field: "",
            operator: "",
            parameter: [
              {
                name: "",
                currIcon: "PlusCircleIcon",
              },
            ],
            amountRev: "",
          },
        ],
      },
      currDescChar: 0,
      revenueList: [],
    };
  },
  methods: {
    countChar() {
      this.currDescChar = this.revenueGroup.desc.length;
    },
    submitForm() {
      this.revenueList.push({
        name: this.revenueGroup.name,
        desc: this.revenueGroup.desc,
        special: this.revenueGroup.special,
        rule: this.revenueGroup.rule.map((x) => ({
          field: x.field,
          operator: x.operator,
          parameter: x.parameter.map((y) => ({
            name: y.name,
            currIcon: y.currIcon,
          })),
          amountRev: x.amountRev + "%",
        })),
      });
      this.$emit("newRevenue", this.revenueList);
      this.resetForm();
    },
    resetForm() {
      this.revenueGroup = {
        name: "",
        desc: "",
        special: false,
        rule: [
          {
            field: "",
            operator: "",
            parameter: [
              {
                name: "",
                currIcon: "PlusCircleIcon",
              },
            ],
            amountRev: "",
          },
        ],
      };
      this.currDescChar = 0;
    },
  },
};
</script>
