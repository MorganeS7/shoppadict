<template>
    <li class="product">
        <img class="product__img" :src="product.img_url">
        <div class="product__description">
            <div class="product__title"><b>{{ product.brand }}</b> - {{ product.name }}</div>
            <div class="product__price">${{ product.price }}</div>
            <router-link :to="'/product/' + product.id"><i class="fas fa-search"></i></router-link>
        </div>
    </li>
</template>

<script>
export default {
  name: 'ProductItem',
  props: ['product']
}
</script>

<style lang="scss" scoped>
    @import '../../static/styles/mixins.scss';

    .product {
        @include displayFlex;
        @include flexDirectionColumn;
        @include alignItemsCenter;
        @include justifyContentEnd;

        position: relative;
        list-style: none;
        width: 180px;
        height: 300px;

        font-size: 90%;
        margin: 2% 5%;

        color: black;
        text-decoration: none;

        &__img {
            max-width: 90%;
            max-height: 70%;
        }

        &__description {
            height: 30%;
            width: 100%;
            padding: 5px;

            text-overflow: ellipsis;
            overflow: hidden;

            @include displayFlex;
            @include flexDirectionColumn;
            @include alignItemsCenter;
            @include justifyContentEnd;
        }

        &__title {
            max-height: 50%;
            width: inherit;
            white-space: nowrap;
            
            overflow: hidden;
            text-overflow: ellipsis;
        }

        &__price {
            max-height: 33%;
            font-weight: bold;
        }
    }
</style>