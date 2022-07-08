<template>
  <div class="products">

    <c-select 
      class="select" 
      :options="options" 
      :optionIsActive="optionIsActive"
      @option-change="$emit('option-change', $event)"
    />

    <div class="list-products" >
      <card-product 
        v-for="(productItem, index) in products" 
        :key="index"
        :productItem="productItem"
        class="card-product"
        @delete-product="$emit('delete-product',$event)"
      />
    </div>
  </div>
</template>

<script>
import CSelect from './CSelect.vue'
import CardProduct from './CardProduct.vue'

export default {
  name: 'TheProducts',
  props: {
    products: {
      type: Array,
      required: true
    }
  },
  components: {
    CSelect,
    CardProduct
  },
  data() {
    return {
      options: [
        { name: 'По умолчанию', value: 1 },
        { name: 'По цене min', value: 2 },
        { name: 'По цене max', value: 3 },
        { name: 'По наименованию', value: 4 }
      ],
      optionIsActive: { name: 'По умолчанию' },
    }
  },
}
</script>

<style lang="scss" scoped>
@import '@/assets/scss/variables.scss';

  .products {
    width: 100%;
    padding-top: 32px;
  }
  .select {
    margin-left: auto;
    margin-bottom: 16px;
  }
  .list-products {
    width: 100%;
    display: flex;
    justify-content: space-between;
    gap: 16px;
    flex-wrap: wrap;
  }
  .card-product {
    width: calc(100%/3 - 32px/3);

    &:last-child {
      margin-right: auto !important;
    };
    &:nth-child(3n) {
      margin-right: auto !important;
    };

    @media screen and (max-width: 768px) {
      width: calc(100%/2 - 8px);
    }
    @media screen and (max-width: 425px) {
      width: calc(100%/1);
    }
  }
</style>