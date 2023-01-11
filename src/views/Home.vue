<template>
  <div>
    <b-row>
      <b-col cols="12" md="4">
        <bill-data-form :items="items"></bill-data-form>
      </b-col>
      <b-col cols="12" md="8">
        <product-list-table :items="items"></product-list-table>
      </b-col>
    </b-row>
  </div>
</template>

<script>
import { BRow,BCol } from "bootstrap-vue";
import billDataForm from "../components/BillDataForm.vue";
import productListTable from "../components/ProductListTable.vue";

export default {
  components: {
    BRow,
    BCol,
    billDataForm,
    productListTable,
  },
  data() {
    return {
      items: [
        {
          Name: "Suger",
          Price: "40",
          Quentity: "10",
          Total: "",
          Action:""
        },
        {
          Name: "Tea",
          Price: "80",
          Quentity: "1",
          Total: "",
          Action:""
        },
        {
          Name: "solt",
          Price: "10",
          Quentity: "3",
          Total: "",
          Action:""
        },
        {
          Name: "oli",
          Price: "150",
          Quentity: "0",
          Total: "",
          Action:""
        },
        {
          Name: "coffee",
          Price: "100",
          Quentity: "2",
          Total: "",
          Action:""
        }
        
       
      ],
    }
  },
};
</script>

<style>
</style>
