<template>
  <div class="" style="height: 40vh; overflow: auto">
    <span class="rule-title">Rules</span>
    <div class="d-flex justify-content-end align-items-center">
      <b-badge
        class="text-primary"
        style="background: #00f0ff1a; cursor: pointer"
        @click="newRule()"
      >
        <feather-icon icon="PlusIcon" style="" /> Add
      </b-badge>
    </div>
    <div
      v-for="(rule, idx) in rules"
      :key="idx"
      class="mt-3 p-2"
      style="border: 1px dashed grey; border-radius: 5px"
    >
      <div
        class="d-flex flex-wrap justify-content-between align-items-center"
        style="cursor: pointer"
      >
        <span class="rule-sub">Rule {{ idx + 1 }}</span>
        <feather-icon icon="XIcon" style="" @click="deleteRule(idx)" />
      </div>
      <div
        class="d-flex flex-wrap p-2"
        style="background: #e0e0e0; border-radius: 5px; height: 100%"
      >
        <span class="d-flex align-items-center" style="height: 33px">If</span>
        <v-select
          v-model="rule.field"
          :options="fieldList"
          placeholder="Select Field"
          label="text"
          class="ml-2"
          style="width: 30%; height: 100%"
        >
        </v-select>
        <v-select
          v-model="rule.operator"
          :options="operatorList"
          placeholder="Select Operator"
          label="text"
          class="ml-2"
          style="width: 30%; height: 100%"
        >
        </v-select>
        <div class="d-flex flex-column" style="width: 35%">
          <div
            v-for="(param, id) in rule.parameter"
            :key="id"
            class="ml-2 mb-1 d-flex flex-wrap align-items-center"
          >
            <input
              class="dronos-formcontrol"
              placeholder="Enter Parameter"
              style="width: 83%"
              v-model="param.name"
            />
            <feather-icon
              class="ml-1"
              :icon="param.currIcon"
              size="20"
              style="width: 13%; cursor: pointer"
              @click="newParam(rule.parameter, id)"
            />
          </div>
        </div>
      </div>
      <div class="d-flex flex-wrap align-items-center mt-2">
        then revenue is
        <input
          class="dronos-formcontrol-icon ml-3"
          type="number"
          placeholder="Enter Amount"
          style="width: 30%"
          v-model="rule.amountRev"
          onkeydown="javascript: return event.keyCode == 69 || event.keyCode == 189 ? false : true"
        />
      </div>
    </div>
  </div>
</template>
<style>
@import "vue-select/dist/vue-select.css";
</style>
<style scoped>
.rule-title {
  font-size: 20px;
}
.rule-sub {
  font-size: 18px;
}
.dronos-formcontrol {
  outline: none !important;
  border: 1px solid #d3d3d3 !important;
  background: white;
  text-overflow: ellipsis;
  height: 33px;
  padding: 10px;
  background-clip: padding-box;
  border-radius: 5px;
  transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
}
.dronos-formcontrol-icon {
  outline: none !important;
  border: 1px solid #d3d3d3 !important;
  background: white;
  text-overflow: ellipsis;
  height: 33px;
  padding: 10px;
  background-clip: padding-box;
  border-radius: 5px;
  padding-left: 35px;
  transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
  background-image: url("~@/assets/percent.svg");
  background-size: 16px 16px;
  background-repeat: no-repeat;
  background-position-x: 10px;
  background-position-y: 7px;
}
</style>
<script>
import { BBadge } from "bootstrap-vue";
import vSelect from "vue-select";
// import CreateRule from "@/views/Components/CreateRule.vue";

export default {
  components: {
    BBadge,
    vSelect,
  },

  data() {
    return {
      currId: 1,
      fieldList: [
        {
          text: "afff_sub_1",
          value: "afff_sub_1",
        },
        {
          text: "afff_sub_2",
          value: "afff_sub_2",
        },
        {
          text: "afff_sub_3",
          value: "afff_sub_3",
        },
        {
          text: "afff_sub_4",
          value: "afff_sub_4",
        },
      ],
      operatorList: [
        {
          text: "is",
          value: "is",
        },
        {
          text: "is not",
          value: "is not",
        },
        {
          text: "starts with",
          value: "starts with",
        },
        {
          text: "ends with",
          value: "ends with",
        },
        {
          text: "contains",
          value: "contains",
        },
        {
          text: "doesn't contains",
          value: "doesn't contains",
        },
      ],
      tempRule: [],
    };
  },
  props: {
    rules: {
      type: Array,
      default: () => [],
    },
  },
  // mounted() {
  //   this.tempRule = this.rules;
  // },
  updated() {
    this.tempRule = this.rules;
  },
  methods: {
    newParam(params, index) {
      if (index === 0 && params.length !== 3) {
        params.push({
          name: "",
          currIcon: params.length !== 0 ? "MinusCircleIcon" : "PlusCircleIcon",
        });
      } else if (index === 1 || index === 2) {
        params.splice(index, 1);
      }
    },
    newRule() {
      // eslint-disable-next-line vue/no-mutating-props
      this.rules.push({
        field: "",
        operator: "",
        parameter: [
          {
            name: "",
            currIcon: "PlusCircleIcon",
          },
        ],
        amountRev: "",
      });
    },
    deleteRule(index) {
      // eslint-disable-next-line vue/no-mutating-props
      this.rules.splice(index, 1);
    },
  },
};
</script>
