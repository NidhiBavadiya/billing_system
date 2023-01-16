<template>
  <b-card-code no-body title="Basic Table">
    <!-- table for bill data display -->
    <b-table
      responsive="sm"
      :fields="fields"
      :items="billdata"
      :b_Slip="data.b_Slip"
      >
      <template #cell(action)="data">
        <!-- Action button -->
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
        <!-- row for display total , discount , payprice -->
        <tr>
          <td colspan="3" class="text-center">Total</td>
          <td colspan="2">
            {{ totalPrice }}
          </td>
        </tr>
        <tr>
          <td colspan="3" class="text-center">Discount</td>
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
    // function for calculate total
    totalPrice() {
      this.totalP = this.billdata.reduce((acc, item) => acc + item.Total, 0);
      return this.totalP;
    },
    // function for discount with condition
    discount() {
      if (this.totalP <= 500) {
        this.discount_amt = (10 / 100) * this.totalP;
        console.log("discount_10_amt", this.discount_amt);
        return this.discount_amt;
      } else if (this.totalP >= 500 && this.totalP <= 1000) {
        this.discount_amt = (15 / 100) * this.totalP;
        console.log("discount_15_amt", this.discount_amt);
        return this.discount_amt;
      } else if (this.totalP >= 1000 && this.totalP <= 1500) {
        this.discount_amt = (20 / 100) * this.totalP;
        console.log("discount_20_amt", this.discount_amt);
        return this.discount_amt;
      } else if (this.totalP >= 1500 && this.totalP <= 10000) {
        this.discount_amt = (25 / 100) * this.totalP;
        console.log("discount_25_amt", this.discount_amt);
        return this.discount_amt;
      }
    },
    // function for total pay values
    payment() {
      this.totalPay = this.totalP - this.discount_amt;
      return this.totalPay;
    },
  },
  // set watcher for inc /dec change value then change total
  watch: {
    Quentity() {
      let total = id.Price * id.Quentity;
      this.Total = total;
    },
  },

  methods: {
    // methid for inc value
    increment(id) {
      let Qun = (id.Quentity ++);
      id.Total = id.Price * Qun;
    },

    //method for dec value
    decrement(id) {
      if (id.Quentity <= 1) {
        this.billdata.splice(this.billdata.indexOf(id), 1);
      } else {
        let Qun = (id.Quentity -= 1);
        id.Total -= id.Price;
        console.log("Qun", Qun);
      }
    },
    //submit button
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
      this.data.b_Slip = this.finalBill;
      this.$router.push("/bill");
      this.finalBill = {
        product: null,
        price: null,
        Total: null,
        Discount: null,
        pay: null,
        id: null,
      };
    },
  },
};
</script>
<style lang="scss">
@import "@core/scss/vue/libs/vue-select.scss";
</style>