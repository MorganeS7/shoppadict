<template>
  <div class="container" id="app">
    <Header v-bind:filters="filters"></Header>
    <Sidebar v-bind:filters="filters"></Sidebar>
    <router-view v-bind:filters="filters"></router-view>
  </div>
</template>

<script>
import Products from './components/Products'
import Header from './components/Header'
import Sidebar from './components/Sidebar'

export default {
  name: 'app',
  components: {
    Products,
    Header,
    Sidebar
  },
  data () {
    return {
      filters: {
        color: '',
        brand: '',
        price: '',
        mainCat: '',
        subCat: '',
        lastCat: '',
        search: ''
      }
    }
  },
  methods: {
  }
}
</script>

<style lang="scss" scoped>
  @import '../static/styles/mixins.scss';

  body {
    margin: 0;
    padding: 0;
  }

  .container {
    font-family: 'Slabo 27px', serif;
    @include displayFlex;
    @include flexWrap;
  }
</style>