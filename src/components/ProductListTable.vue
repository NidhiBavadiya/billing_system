<template>
  <b-card-code no-body title="Basic Table">
    <b-table responsive="sm" :fields="fields" :items="billdata" :billSlip="data.billSlip">  <!--:billSlip="billSlip"-->
    
      <template #cell(action)="data">
        <feather-icon
          class="cursor-pointer"
          icon="PlusSquareIcon"
          size="20"
          color="#7367f0"
          @click="increment(data.item.Quentity)"
        >
        </feather-icon>
        <feather-icon
          class="ml-1 cursor-pointer"
          icon="MinusSquareIcon"
          size="20"
          color="#7367f0"
          @click="decrement(data.item.Quentity)"
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
import data from '../assets/data.json'

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
      Name:"",
      totalP: "",
      discount_amt: "",
      totalPay: "",
      finalBill: "",

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

  methods: {
    increment(Quentity) {
      console.log("Quentity",Quentity);
      Quentity +=1;
      console.log("inc",Quentity);
     
    },
    decrement(Quentity) {
      console.log("Quentity",Quentity);
      if (Quentity <= 0) {
        Quentity = 0;
      } else {
        Quentity -= 1;
        console.log("dec",Quentity);
      }
    },
    submitBill() {
      this.finalBill = {
        product: this.billdata[0].Name,
        price : this.billdata[0].Price,
        Total: this.totalP,
        Discount: this.discount_amt,
        pay: this.totalPay,
        id:this.id
      };
      console.log("finalBill", this.finalBill);
      this.data.billSlip.push(this.finalBill);
      this.$router.push("/second-page");
    },
  },
};


</script>
<style lang="scss">
@import "@core/scss/vue/libs/vue-select.scss";
</style>