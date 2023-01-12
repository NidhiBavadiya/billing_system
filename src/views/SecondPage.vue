<template>
  <div>
    <b-card class="w-50 p-4">
      <!-- product & price -->
      <b-row class="justify-content-between">
        <b-col cols="12" md="4" class="mt-2 pl-1 p-0">
          <h4>Product</h4>

          <ul v-for="i in this.productBill[0].products" :key="i.Name" class=" p-0 ul_data">
          <li class="pt-1">{{i.Name}}</li>
          </ul>
        </b-col>
        <b-col cols="12" md="4" class="mt-2 justify-content-right ">
          <h4 style="text-align:right">Price</h4>
          <ul v-for="i in this.productBill[0].products" :key="i.Name" style=" text-align: right;" class="p-0 ul_data">
          <li class="pt-1">{{i.Total}}</li>
          </ul>
        </b-col>
      </b-row>
      <hr class="m-0">
      <!-- Total -->
      <b-row>
        <b-col cols="12" md="12" class="mt-1">
          <div class="d-flex justify-content-between">
            <h4>Total</h4>
            <p>{{ productBill[0].Total }}</p>
          </div>
        </b-col>
      </b-row>
      <hr class="m-0">
      <!-- Discount price -->
      <b-row>
        <b-col cols="12" md="12" class="mt-1">
          <div class="d-flex justify-content-between">
            <h4>Discount</h4>
            <p>{{ productBill[0].Discount }}</p>
          </div>
        </b-col>
      </b-row>
      <hr class="m-0">
      <!-- pay Price -->
      <b-row>
        <b-col cols="12" md="12" class="mt-1">
          <div class="d-flex justify-content-between">
            <h4>pay</h4>
            <p>{{ productBill[0].pay }}</p>
          </div>
        </b-col>
      </b-row>
    </b-card>
  </div>
</template>

<script>
import { BCard, BRow, BCol } from "bootstrap-vue";
import data from "../assets/data.json";
export default {
  components: {
    BCard,
    BRow,
    BCol,
  },
  data() {
    return {
      data: data,
      productBill: "",
      allProductBill: "",
    };
  },
  //data receive from product list component
  mounted() {
    this.productBill = this.data.billSlip;
    console.log("...thisproductBill", this.productBill);
  },
};
</script>

<style>
.ul_data{
  list-style: none;

}
</style>
