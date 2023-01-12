
 
<template>
  <b-card>
    <h2 class="mb-3">Single Product Detail</h2>
    <b-form @submit.prevent ref="clearform">
      <b-row>
        <!-- Product Name -->
        <b-col cols="12">
          <b-form-group label="Product Name">
            <v-select
              v-model="Name"
              :dir="$store.state.appConfig.isRTL ? 'rtl' : 'ltr'"
              label="Name"
              :options="data.items"
            />
          </b-form-group>
        </b-col>
      </b-row>
      <b-row>
        <!-- Price-->
        <b-col cols="12" md="6">
          <b-form-group label="Price" label-for="v-Price">
            <b-form-input
              id="v-Price"
              type="number"
              label="Price"
              v-model="Name.Price"
            />
          </b-form-group>
        </b-col>

        <!-- Quentity -->
        <b-col cols="12" md="6">
          <b-form-group label="Quentity" label-for="v-quentity">
            <b-input-group>
              <b-input-group-append>
                <b-button
                  variant="outline-primary"
                  v-ripple.400="'rgba(255, 255, 255, 0.15)'"
                  @click="decrement"
                  class="p10px"
                >
                  -
                </b-button>
              </b-input-group-append>
              <b-form-input
                class="p-0 text-center"
                id="v-quentity"
                v-model="Quentity"
              ></b-form-input>

              <b-input-group-append>
                <b-button
                  variant="outline-primary"
                  v-ripple.400="'rgba(255, 255, 255, 0.15)'"
                  @click="increment"
                  class="p10px"
                >
                  +
                </b-button>
              </b-input-group-append>
            </b-input-group>
          </b-form-group>
        </b-col>
      </b-row>
      <b-row>
        <!-- Total -->
        <b-col cols="12">
          <b-form-group label="Total" label-for="v-total">
            <b-form-input
              id="v-total"
              type="number"
              placeholder="Total"
              v-model="Total"
              disabled
            ></b-form-input>
          </b-form-group>
        </b-col>
      </b-row>
      <!--Add -->
      <b-row>
        <b-col cols="12" class="mt-3">
          <b-button
            v-ripple.400="'rgba(255, 255, 255, 0.15)'"
            type="submit"
            variant="primary"
            class="mr-1"
            @click="AddData()"
          >
            Add
          </b-button>
        </b-col>
      </b-row>
    </b-form>
  </b-card>
</template>
  
<script>
import {
  BRow,
  BCol,
  BFormGroup,
  BFormInput,
  BFormCheckbox,
  BInputGroup,
  BForm,
  BButton,
  BCard,
  BInputGroupAppend,
} from "bootstrap-vue";
import Ripple from "vue-ripple-directive";
import vSelect from "vue-select";
import data from "../assets/data.json";
export default {
  components: {
    BRow,
    BCol,
    BFormGroup,
    BFormInput,
    BFormCheckbox,
    BForm,
    BButton,
    BCard,
    BInputGroup,
    BInputGroupAppend,
    vSelect,
  },
  directives: {
    Ripple,
  },

  data() {
    return {
      Name: "",
      Price: "",
      Total: "",
      Quentity:null,

      data: data,
    };
  },

  watch: {
    Quentity() {
      if (this.Name) {       
      }
      let total = this.Name.Price * this.Name.Quentity;
      this.Total = total;
      
    },
    Name() {
      this.Quentity()
    },
  },
  methods: {
    increment() {
      this.Name.Quentity++;
      let Qun = this.Name.Quentity;
      this.Quentity = Qun;
    },
    decrement() {
      if (this.Name.Quentity <= 0) {
        this.Name.Quentity = 0;
        // this.data.item.splice(this.data.items); 
      } else {
        this.Name.Quentity -= 1;
      }
      let Qun = this.Name.Quentity;
      this.Quentity = Qun;
    },

    AddData() {
      let billValue = {
        Name: this.Name.Name,
        Price: this.Name.Price,
        Total: this.Total,
        Quentity: this.Quentity,
        id: this.Name.id,
      };
      this.$emit("adddata", billValue);
      this.$refs.clearform.reset();
      billValue = {
        Name: null,
        Price: null,
        Total: null,
        Quentity: null,
        id: null,
      };
    },
  },
};
</script>
<style lang="scss">
@import "@core/scss/vue/libs/vue-select.scss";

.p10px {
  padding: 10px;
}
</style>