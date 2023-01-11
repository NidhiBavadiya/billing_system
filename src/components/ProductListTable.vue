<template>
  <b-card-code no-body title="Basic Table">
    <b-table responsive="sm" :items="items">
      <template #cell(action)>
        <feather-icon
          class="cursor-pointer"
          icon="PlusSquareIcon"
          size="20"
          color="#7367f0"
          @click="increment()"
        >
        </feather-icon>
        <feather-icon
          class="ml-1 cursor-pointer"
          icon="MinusSquareIcon"
          size="20"
          color="#7367f0"
          @click="decrement()"
        >
        </feather-icon>
      </template>
    </b-table>
  </b-card-code>
</template>
  
  <script>
import BCardCode from "@core/components/b-card-code/BCardCode.vue";
import { BTable } from "bootstrap-vue";

export default {
  components: {
    BCardCode,
    BTable,
  },
  props: {
    items: Array,
  },
  data() {
    return {
      value: 0,
    };
  },
  methods: {
    increment() {
      this.value += 1;
    },
    decrement() {
      if (this.value <= 0) {
        this.value = 0;
      } else {
        this.value -= 1;
      }
    },
  },
};
</script>
  