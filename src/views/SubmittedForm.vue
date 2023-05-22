<template>
  <div class="p-1">
    <div class="">
      <span class="h4 d-flex mb-5">Browse Revenue Groups</span>
      <div v-if="revenueDisplay.length === 0">No data</div>
      <div v-for="(dataRevenue, index) in revenueDisplay" :key="index">
        <div
          class="mb-1"
          style="
            box-shadow: 0px 0px 4px rgba(0, 0, 0, 0.35);
            border-radius: 6px;
            width: 100%;
          "
        >
          <div
            class="d-flex justify-content-between align-items-center p-3"
            style="width: 100%; height: 70px"
          >
            <div
              class="d-flex flex-wrap align-items-center ml-1"
              style="width: 100%; height: 100%"
            >
              <span class="label-table">{{ dataRevenue.name }}</span>
              <b-badge
                variant="primary"
                class="p-1 ml-2"
                style="color: white; border-radius: 50px; cursor: pointer"
                @click="newRule()"
              >
                <span class="m-1" v-if="dataRevenue.special === true">
                  Special Group
                </span>
              </b-badge>
            </div>
            <div style="cursor: pointer" class="" @click="deleteRevenue(index)">
              <img
                src="@/assets/Iconsdelete.svg"
                class="p-1"
                style="background: lightgrey; border-radius: 50%"
              />
              <!-- <feather-icon icon="PlusIcon" style="" /> -->
            </div>
          </div>
          <span class="d-flex ml-3">{{ dataRevenue.desc }}</span>
          <b-table
            style="color: white"
            :items="dataRevenue.rule"
            :fields="fields"
            striped
            selected-variant="primary"
            :responsive="true"
            hover
            class="mt-4"
            show-empty
          >
            <template #cell(rule)="data">
              <span>{{ data.index + 1 }}</span>
            </template>
            <template #cell(parameter_1)="data">
              <span>{{
                data.item.parameter[0] === undefined
                  ? ""
                  : data.item.parameter[0].name
              }}</span>
            </template>
            <template #cell(parameter_2)="data">
              <span>{{
                data.item.parameter[1] === undefined
                  ? ""
                  : data.item.parameter[1].name
              }}</span>
            </template>
            <template #cell(parameter_3)="data">
              <span>{{
                data.item.parameter[2] === undefined
                  ? ""
                  : data.item.parameter[2].name
              }}</span>
            </template>
            <template #cell(action)="data">
              <div
                style="cursor: pointer"
                @click="deleteRule(index, data.index)"
              >
                <i class="fa-solid fa-trash" style="color: #8a8e99"></i>
              </div>
            </template>
          </b-table>
        </div>
      </div>
    </div>
  </div>
</template>
<style>
.table-striped > tbody > tr:nth-child(2n + 1) > td,
.table-striped > tbody > tr:nth-child(2n + 1) > th {
  background-color: rgba(118, 171, 255, 0.3);
}
</style>
<script>
import { BTable, BBadge } from "bootstrap-vue";

export default {
  components: {
    BTable,
    BBadge,
  },

  data() {
    return {
      currRevenueData: null,
      fields: [
        {
          label: "Rule",
          key: "rule",
          sortable: true,
        },
        {
          label: "Field",
          key: "field.text",
          sortable: true,
        },
        {
          label: "Operator",
          key: "operator.text",
          sortable: true,
        },
        {
          label: "Parameter 1",
          key: "parameter_1",
          sortable: true,
        },
        {
          label: "Parameter 2",
          key: "parameter_2",
          sortable: true,
        },
        {
          label: "Parameter 3",
          key: "parameter_3",
          sortable: true,
        },
        {
          label: "Revenue",
          key: "amountRev",
          sortable: true,
        },
        {
          label: "Action",
          key: "action",
        },
      ],
      revenueDisplay: [],
      revenueGroup: {
        name: "pe",
        desc: "",
        special: true,
        rule: [
          {
            field: "aff_sub_1",
            operator: "contains",
            parameter: [
              {
                name: "Lorem ipsum",
                currIcon: "PlusCircleIcon",
              },
            ],
            amountRev: "10%",
          },
        ],
      },
    };
  },
  props: {
    revenueList: {
      type: Array,
      default: () => [],
    },
  },
  watch: {
    revenueList: {
      handler(val) {
        console.log(val);
        this.revenueDisplay = val;
      },
    },
  },
  mounted() {
    console.log("masuk ke");
  },
  methods: {
    deleteRule(revIndex, index) {
      console.log(this.revenueDisplay[revIndex].rule, revIndex, index);
      this.revenueDisplay[revIndex].rule.splice(index, 1);
    },
    deleteRevenue(index) {
      console.log(this.revenueDisplay, index);
      this.revenueDisplay.splice(index, 1);
    },
  },
};
</script>
