<template>
  <b-card-code no-body title="Basic Table">
    <b-table
      responsive="sm"
      :fields="fields"
      :items="billdata"
      :billSlip="data.billSlip"
    >
      <!--:billSlip="billSlip"-->
      <!-- <template #cell(Quentity)></template> -->
      <template #cell(action)="data">
        <feather-icon
          class="cursor-pointer"
          icon="PlusSquareIcon"
          size="20"
          color="#7367f0"
          @click="increment(data.item)"
        >
        </feather-icon>
        <feather-icon
          class="ml-1 cursor-pointer"
          icon="MinusSquareIcon"
          size="20"
          color="#7367f0"
          @click="decrement(data.item)"
        >
        </feather-icon>
      </template>
      <template #custom-foot>
        <tr>
          <td colspan="3" class="text-center">Total</td>
          <td colspan="2">
            {{ totalPrice }}
          </td>
        </tr>
        <tr>
          <td colspan="3" class="text-center">10% Discount</td>
          <td colspan="2">
            {{ discount }}
          </td>
        </tr>
        <tr>
          <td colspan="3" class="text-center">Pay</td>
          <td>
            {{ payment }}
          </td>
          <td>
            <b-button
              v-ripple.400="'rgba(255, 255, 255, 0.15)'"
              type="submit"
              variant="primary"
              class="mr-1"
              @click="submitBill()"
            >
              Submit
            </b-button>
          </td>
        </tr>
      </template>
    </b-table>
  </b-card-code>
</template>
  
  <script>
import BCardCode from "@core/components/b-card-code/BCardCode.vue";
import { BTable, BButton } from "bootstrap-vue";
import Ripple from "vue-ripple-directive";
import data from "../assets/data.json";

export default {
  components: {
    BCardCode,
    BTable,
    BButton,
  },
  directives: {
    Ripple,
  },
  props: {
    billdata: Array,
    fields: Array,
  },
  mounted() {
    console.log("Array", this.billdata);
  },
  data() {
    return {
      Name: "",
      Quentity: "",
      totalP: "",
      discount_amt: "",
      totalPay: "",
      finalBill: "",
      abcd: [],
      data: data,
    };
  },

  computed: {
    totalPrice() {
      this.totalP = this.billdata.reduce((acc, item) => acc + item.Total, 0);
      return this.totalP;
    },
    discount() {
      this.discount_amt = (10 / 100) * this.totalP;
      return this.discount_amt;
    },
    payment() {
      this.totalPay = this.totalP - this.discount_amt;
      return this.totalPay;
    },
  },
  watch: {
    Quentity() {
      let total = id.Price * id.Quentity;
      this.Total = total;
    },
  },
  methods: {
    increment(id) {
      console.log("Array id", id.Quentity);
      let Qun = (id.Quentity += 1);
      console.log("Qun", Qun);
      id.Total = id.Price * Qun;
    },
    decrement(id) {
      console.log("Array id", id);
      if (id.Quentity <= 0) {
        this.billdata.splice(id, 1)
      } else {
        console.log("Array id", id);
        let Qun = (id.Quentity -= 1);
        console.log(Qun);
        id.Total -= id.Price;
      }
    },
    submitBill() {
      this.b_data = this.billdata;
      this.finalBill = [
        {
          product: this.b_data,
          price: this.b_data,
          Total: this.totalP,
          Discount: this.discount_amt,
          pay: this.totalPay,
          id: this.id,
        },
      ];
      console.log("finalBill", this.finalBill);
      this.data.billSlip = this.finalBill;
      this.$router.push("/second-page");
    },
  },
};
</script>
<style lang="scss">
@import "@core/scss/vue/libs/vue-select.scss";
</style>