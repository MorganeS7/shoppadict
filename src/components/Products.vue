<template>
    <ul class="products">
        <product-item
            v-for="product in filteredProducts"
            v-bind:product="product"
            v-bind:key="product.id">
        </product-item>
    </ul>
</template>

<script>
import ProductItem from './ProductItem';

export default {
  name: 'Products',
  props: {
    filters: {
      required: false
    }
  },
  components: {
      ProductItem
  },
  data() {
    return {
      products: [],
      productsList: []
    }
  },
  methods: {
    getProducts: function() {
      this.$http.get('http://localhost:3000/products')
       .then(response => {
         this.products = response.data;
       });
    }
  },
  created: function() {
    this.getProducts();
  },
  computed: {
    filteredProducts: function() {
      this.productsList = this.products;
      if (this.filters.search !== '') {
        this.productsList = this.productsList.filter(product => {
              return product.name.toLowerCase().includes(this.filters.search)
        });
      }

      if (this.filters.price !== '') {
        this.productsList = this.productsList.filter(product => {
          return (parseInt(product.price) < this.filters.price) ? product : ''
        });
      }

      if (this.filters.color !== '') {
        this.productsList = this.productsList.filter(product => {
              return (product.color == this.filters.color) ? product : ''
        });
      }

      if (this.filters.brand !== '') {
        this.productsList = this.productsList.filter(product => {
              return (product.brand == this.filters.brand) ? product : ''
        });
      } 

      if (this.filters.mainCat !== '') {
        this.productsList = this.productsList.filter(product => {
              return (product.main_category == this.filters.mainCat) ? product : ''
        });
      }

      if (this.filters.subCat !== '') {
        this.productsList = this.productsList.filter(product => {
              return (product.main_category == 'woman' && product.sub_category == this.filters.subCat) ? product : ''
        });
      }

      if (this.filters.lastCat !== '') {
        this.productsList = this.productsList.filter(product => {
              return (product.main_category == 'woman' && product.last_category == this.filters.lastCat) ? product : ''
        });
      }

      return this.productsList;
    }
  } 
}


</script>

<style lang="scss" scoped>
  @import '../../static/styles/mixins.scss';
  .products {
    margin-top: 50px;

    width: 70%;

    @include displayFlex;
    @include flexWrap;

    @media screen and (max-width: 1000px) {
      width:60%;
    }

    @media screen and (max-width: 700px) {
      width:50%;
    }
  }
</style>