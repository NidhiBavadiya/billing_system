
 
<template>
  <b-card>
    <h2 class="mb-3">Simgle Product Detail</h2>
    <b-form @submit.prevent>
      <b-row>
        <!-- Product Name -->
        <b-col cols="12">
          <b-form-group label="Product Name">
            <v-select
              v-model="selected"
              :dir="$store.state.appConfig.isRTL ? 'rtl' : 'ltr'"
              label="Name"
              :options="items"
            />
          </b-form-group>
        </b-col>
      </b-row>
      <b-row>
        <!-- Price-->
        <b-col cols="12" md="6">
          <b-form-group label="Price" label-for="v-price">
            <b-form-input id="v-price" type="price" label="price" />
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
                  @click="increment"
                >
                  +
                </b-button>
              </b-input-group-append>
              <b-form-input
                id="v-quentity"
                type="quentity"
                v-model="Quality"
              ></b-form-input>

              <b-input-group-append>
                <b-button
                  variant="outline-primary"
                  v-ripple.400="'rgba(255, 255, 255, 0.15)'"
                  @click="decrement"
                >
                  -
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
            <b-form-input id="v-total" type="total" />
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

  props: {
    items: Array,
  },
  data() {
    return {
      selected: null,
      Name: "",
      Price: "",
      // Quality:'',
      Total: "",
      Quality: 0,
    };
  },
  methods: {
    increment() {
      this.Quality += 1;
    },
    decrement() {
      if (this.Quality <= 0) {
        this.Quality = 0;
      } else {
        this.Quality -= 1;
      }
    },
  },
};
</script>
<style lang="scss">
@import "@core/scss/vue/libs/vue-select.scss";
</style>