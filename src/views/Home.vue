<template>
  <div>
    <b-row>
      <b-col cols="12" md="4">
        <bill-data-form @adddata="bill"></bill-data-form>
      </b-col>
      <b-col cols="12" md="8">
        <product-list-table
          :fields="fields"
          :billdata="billdata"
        ></product-list-table>
      </b-col>
    </b-row>
  </div>
</template>

<script>
import { BRow, BCol } from "bootstrap-vue";
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
      billdata: [],
      fields: [
        {
          value:"Name",
          key:"Name"
        },
        {
          value:"Price",
          key:"Price"
        },
        {
          value:"Quentity",
          key:"Quentity"
        },
        {
          value:"Total",
          key:"Total"
        },
        {
          value:"Action",
          key:"action"
        },
      ],
    };
  },
  mounted(){
    data.items.forEach(item => {
        if(item.id === billValue.id){
          console.log("Item already exist")
        }
        else{
          this.$emit("adddata", billValue); 
        }
        console.log("item...",item.id);
        console.log("....",billValue.id);
      });
  },
  methods: {
    bill(value) {
      console.log(value);
      this.billdata.push(value)
      console.log("billData", this.billdata);
    },
  },
};
</script>

<style>
</style>
