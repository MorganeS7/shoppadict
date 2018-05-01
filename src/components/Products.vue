<template>
    <ul class="products">
        <product-item
            v-for="product in productsList"
            v-bind:product="product"
            v-bind:key="product.id">
        </product-item>
    </ul>
</template>

<script>
import ProductItem from './ProductItem'
import {SearchBus, PriceBus, BrandBus, ColorBus, MainCatBus, SubCatBus, LastCatBus} from '../buses/buses.js';

export default {
  name: 'Products',
  components: {
      ProductItem
  },
  data() {
    return {
      products: [],
      productsList: [],
      search: '',
      price: '',
      brand: '',
      color: ''
    }
  },
  methods: {
    getProducts: function() {
      this.$http.get('http://localhost:3000/products')
       .then(response => {
         this.products = response.data;
         this.productsList = response.data;
       });
    }
  },
  created: function() {
    this.getProducts();
  },
  updated: function() {
    SearchBus.$on('searching', searchText => {
      this.search = searchText;
      this.productsList = this.products.filter(product => {
            return product.name.toLowerCase().includes(this.search)
      });
    });

    PriceBus.$on('price-request', priceFilter => {
      this.price = priceFilter;
      if (this.price) {
          this.productsList = this.products.filter(product => {
            return (parseInt(product.price) < this.price) ? product : ''
          });

          if (this.color) {
            this.productsList = this.productsList.filter(product => {
                  return (product.color == this.color) ? product : ''
            });
          }

          if (this.brand) {
            this.productsList = this.productsList.filter(product => {
                  return (product.brand == this.brand) ? product : ''
            });
          }
      } else {
        this.productsList = this.products;

        if (this.color) {
          this.productsList = this.productsList.filter(product => {
                return (product.color == this.color) ? product : ''
          });
        }

        if (this.brand) {
          this.productsList = this.productsList.filter(product => {
                return (product.brand == this.brand) ? product : ''
          });
        }
      }
    });

    ColorBus.$on('color-request', colorFilter => {
      this.color = colorFilter;
      if (this.color) {
        this.productsList = this.products.filter(product => {
              return (product.color == this.color) ? product : ''
        });

        if (this.brand) {
          this.productsList = this.productsList.filter(product => {
                return (product.brand == this.brand) ? product : ''
          });
        }

        if (this.price) {
          this.productsList = this.productsList.filter(product => {
            return (parseInt(product.price) < this.price) ? product : ''
          });
        }
      } else {
        this.productsList = this.products;

        if (this.brand) {
          this.productsList = this.productsList.filter(product => {
                return (product.brand == this.brand) ? product : ''
          });
        }

        if (this.price) {
          this.productsList = this.productsList.filter(product => {
            return (parseInt(product.price) < this.price) ? product : ''
          });
        }
      }
    });

    BrandBus.$on('brand-request', brandFilter => {
      this.brand = brandFilter;
      if (this.brand) {
        this.productsList = this.products.filter(product => {
              return (product.brand == this.brand) ? product : ''
        });

        if (this.color) {
          this.productsList = this.productsList.filter(product => {
                return (product.color == this.color) ? product : ''
          });
        }

        if (this.price) {
          this.productsList = this.productsList.filter(product => {
            return (parseInt(product.price) < this.price) ? product : ''
          });
        }
      } else {
        this.productsList = this.products;

        if (this.color) {
          this.productsList = this.productsList.filter(product => {
                return (product.color == this.color) ? product : ''
          });
        }

        if (this.price) {
          this.productsList = this.productsList.filter(product => {
            return (parseInt(product.price) < this.price) ? product : ''
          });
        }
      }
    });

    MainCatBus.$on('main-cat-request', name => {
      if (name) {
        this.productsList = this.products.filter(product => {
              return (product.main_category == name) ? product : ''
        });
      } else {
        this.productsList = this.products;
      }
    });

    SubCatBus.$on('sub-cat-request', name => {
      if (name) {
        this.productsList = this.products.filter(product => {
              return (product.main_category == 'woman' && product.sub_category == name) ? product : ''
        });
      } else {
        this.productsList = this.products;
      }
    });

    LastCatBus.$on('last-cat-request', name => {
      if (name) {
        console.log('ici');
        this.productsList = this.products.filter(product => {
              return (product.main_category == 'woman' && product.last_category == name) ? product : ''
        });
      } else {
        this.productsList = this.products;
      }
    });
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