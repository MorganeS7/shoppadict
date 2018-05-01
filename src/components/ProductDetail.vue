<template>
    <div class="product">
        <img class="product__image" :src="product.img_url">
        <div class="product__description">
            <div class="product__breadcrumb">{{product.main_category.toUpperCase()}} / {{product.sub_category.toUpperCase()}} / {{product.last_category.toUpperCase()}}</div>
            <div class="product__brand">{{product.brand}}</div>
            <div class="product__name">{{product.name}}</div>
            <div class="product__color">Color: {{product.color}}</div>
            <div class="product__price">Price: ${{product.price}}</div>
            <div class="product__button">Shop NOW</div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'ProductDetail',
  data() {
    return {
      products: [],
      product: {}
    }
  },
  methods: {
    getProducts: function() {
      this.$http.get('http://localhost:3000/products')
       .then(response => {
         this.products = response.data;
         this.product = this.products[this.$route.params.id];
       });
    }
  },
  created: function() {
    this.getProducts();
  },
}
</script>

<style lang="scss" scoped>
     @import '../../static/styles/mixins.scss';

    .product {
        @include displayFlex;
        @include justifyContentBetween;
        margin-top: 50px;
        width: 70%;

        &__image {
            margin-left: 30px;
            max-width: 50%;
            max-height: 500px;
        }

        &__description {
            width: 50%;
            padding: 10px;

            @include displayFlex;
            @include alignItemsCenter;
            @include flexDirectionColumn;
            text-align: center;

            font-size: 15px;

            & div {
                margin-bottom: 10px;
            }
        }

        &__breadcrumb {
            font-style: italic;
            font-size: 10px;
        }

        &__brand {
            font-weight: bold;
            font-size: 20px;
        }

        &__price {
            font-size: 20px;
            font-weight: bold;
        }

        &__button {
            background-color: #e5aaff;
            border-radius: 2px;
            color: white;

            cursor: pointer;

            width: 50%;
            height: 50px;
            line-height: 50px;
            font-size: 20px;
            font-weight: bold;

            margin-top: 50px;
        }
    }
</style>