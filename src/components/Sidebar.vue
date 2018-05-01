<template>
    <div class="sidebar">
        <div class="sidebar__filter sidebar__filter--brand">
            <div class="sidebar__title">Pick your favorite brand :</div>
            <div v-for="brand in brandList" :key="brand.id">
                <input type="radio" :id="brand" :value="brand" v-model="brandFilter"><label :for="brand">{{brand}}</label>
            </div>
            <div>
                <input type="radio" id="all" value="" v-model="brandFilter"><label :for="price">All</label>
            </div>
        </div>

        <div class="sidebar__filter sidebar__filter--price">
            <div class="sidebar__title">Pick your price range :</div>
            <div v-for="price in priceList" :key="price.id">
                <input type="radio" :id="price" :value="price" v-model="priceFilter"><label :for="price">{{price}}</label>
            </div>
            <div>
                <input type="radio" id="all" value="" v-model="priceFilter"><label :for="price">All</label>
            </div>
        </div>

        <div class="sidebar__filter sidebar__filter--color">
            <div class="sidebar__title">Pick your color :</div>
            <div v-for="color in colorList" :key="color.id">
                <input type="radio" :id="color" :value="color" v-model="colorFilter"><label :for="color">{{color}}</label>
            </div>
            <div>
                <input type="radio" id="all" value="" v-model="colorFilter"><label :for="color">All</label>
            </div>
        </div>
    </div>
</template>

<script>
import {PriceBus} from '../buses/buses.js';
import {BrandBus} from '../buses/buses.js';
import {ColorBus} from '../buses/buses.js';

export default {
  name: 'Sidebar',
  data() {
    return {
      products: [],
      brandList: [],
      priceList: [100, 500, 1000, 5000],
      colorList: [],
      brandFilter: '',
      colorFilter: '',
      priceFilter: '',
      price: null,
      color: null,
      brand: null
    }
  },
  methods: {
    getProducts: function() {
      this.$http.get('http://localhost:3000/products')
       .then(response => {
         this.products = response.data;

         for (var i = 0; i < this.products.length; i++) {
             if (this.colorList.indexOf(this.products[i].color) === -1) {
                 this.colorList.push(this.products[i].color);
             }
             if (this.brandList.indexOf(this.products[i].brand) === -1) {
                 this.brandList.push(this.products[i].brand);
             }
         }
       });
    },
    emitGlobalPriceEvent() {
        PriceBus.$emit('price-request', this.priceFilter);
    },
    emitGlobalColorEvent() {
        ColorBus.$emit('color-request', this.colorFilter);
    },
    emitGlobalBrandEvent() {
        BrandBus.$emit('brand-request', this.brandFilter);
    }
  },
  created: function() {
    this.getProducts();
  },
  watch: {
      priceFilter: function() {
          this.emitGlobalPriceEvent();
      },
      colorFilter: function() {
          this.emitGlobalColorEvent();
      },
      brandFilter: function() {
          this.emitGlobalBrandEvent();
      }
  }
}
</script>

<style lang="scss" scoped>
    @import '../../static/styles/mixins.scss';

    .sidebar {
        width: 20%;
        height: 130vh;

        padding: 50px 0 0 50px;
        margin-top: 0px;

        @include displayFlex;
        @include justifyContentCenter;
        @include flexWrap;

        background-image: url('/static/bg.svg');
        background-size: cover;
        background-repeat: no-repeat;

        &__filter {
            width: 100%;
        }

        &__title {
            font-family: 'Permanent Marker', cursive;
        }
    }

</style>