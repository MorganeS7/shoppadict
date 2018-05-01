<template>
    <header>
        <div class="header">
            <a class="header__brand" href="/">
                <img src="/static/diamond.svg">
                <h1>SHOPADDICT</h1>
            </a>
            <input class="header__search-bar" v-model="searchText" type="text" placeholder="Search by product name...">
        </div>
        <div class="navbar">
            <div class="navbar__link"><span @click="filterMainCat('woman')">WOMAN</span>
                <div class="navbar__dropdown">
                    <div class="navbar__sublink" @click="filterSubCat('clothing')">CLOTHING</div>
                    <div class="navbar__sublink--little" @click="filterLastCat('coats')">COATS</div>
                    <div class="navbar__sublink--little" @click="filterLastCat('dresses')">DRESSES</div>
                    <div class="navbar__sublink--little" @click="filterLastCat('tops')">TOPS</div>
                    <div class="navbar__sublink" @click="filterSubCat('shoes')">SHOES</div>
                </div>
            </div>
            <div class="navbar__link" @click="filterMainCat('man')">MAN</div>
            <div class="navbar__link" @click="filterSubCat('bags')">BAGS</div>
            <div class="navbar__link" @click="filterSubCat('accessories')">ACCESSORIES</div>
        </div>
    </header>
</template>

<script>
import {SearchBus, MainCatBus, SubCatBus, LastCatBus} from '../buses/buses.js';

export default {
  name: 'Header',
  data () {
    return {
        searchText: ''
    }
  },
  methods: {
    emitGlobalSearchEvent() {
        SearchBus.$emit('searching', this.searchText);
    },
    filterMainCat: function(name) {
        MainCatBus.$emit('main-cat-request', name);
    },
    filterSubCat: function(name) {
        SubCatBus.$emit('sub-cat-request', name);
    },
    filterLastCat: function(name) {
        LastCatBus.$emit('last-cat-request', name);
    }
  },
  watch: {
      searchText: function() {
          this.emitGlobalSearchEvent();
      }
  }
}
</script>


<style lang="scss" scoped>
    @import '../../static/styles/mixins.scss';

    header {
        width: 100%;
    }

    .header {
        @include displayFlex;
        @include justifyContentAround;
        @include alignItemsCenter;
        @include flexWrap;

        width: 100%;
        height: 100px;

        @media screen and (max-width: 1000px) {
                height: 240px;
        }


        &__brand {
            @include displayFlex;

            color: black;
            text-decoration: none;
            width: 40%;

            @media screen and (max-width: 1000px) {
                width: 100%;
            }

            h1 {
                font-family: 'Permanent Marker', cursive;
                font-size: 40px;
                margin: 0;
                padding: 0;
            }

            img {
                height: 50px;
                margin-right: 3%;
                transform: rotate(20deg);
                transform-origin: 50% 50%;
            }
        }

        &__search-bar {
            padding-left: 2%;
            width: 40%;
            height: 50px;

            @media screen and (max-width: 1000px) {
                width: 100%;
                margin-bottom: 20px;
            }
        }
    }

    .navbar {
        @include displayFlex;
        @include alignItemsCenter;
        background-color: #eee6f4;

        width: 100%;

        &__link {
            cursor: pointer;

            height: 50px;
            width: 300px;

            font-family: 'Permanent Marker', cursive;
            font-size: 20px;
            line-height: 50px;
            text-align: center;

            position: relative;

            &:hover {
                background-color: #d7b6e5;
            }
        }

        &__link:first-child {
            &:hover > .navbar__dropdown {
                display: block;
                width: 100%;
            }
        }

        &__dropdown {
            display: none;
            background-color: #d7b6e5;
            text-align: center;

            position: absolute;
            width: 100%;
        }

        &__sublink {
            font-family: 'Permanent Marker', cursive;
            font-size: 15px;

            &--little {
                font-size: 10px;
                margin-left: 10px;
            }
        }
    }
</style>