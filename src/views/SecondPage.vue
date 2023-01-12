<template>
  <div>
    <b-card class="w-50">
      <!-- product & price -->
      <b-row class="justify-content-between">
        <b-col cols="12" md="6" class="mt-2">
          <h4>Product</h4>
          <p>{{productBill[0].product}}</p>
        </b-col>
        <b-col cols="12" md="6" class="mt-2">
          <h4>Price</h4>
          <p>{{productBill[0].price }}</p>
        </b-col>
      </b-row>
      <!-- Total -->
      <b-row>
        <b-col cols="12" md="12" class="mt-1">
          <div class="d-flex justify-content-between">
            <h4>Total</h4>
            <p>{{ productBill[0].Total }}</p>
          </div>
        </b-col>
      </b-row>
      <!-- Discount price -->
      <b-row>
        <b-col cols="12" md="12" class="mt-1">
          <div class="d-flex justify-content-between">
            <h4>Discount</h4>
            <p>{{ productBill[0].Discount }}</p>
          </div>
        </b-col>
      </b-row>
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
    };
  },
  //data receive from product list component  
  mounted() {
    this.productBill = this.data.billSlip;
  },
};
</script>

<style>
</style>
