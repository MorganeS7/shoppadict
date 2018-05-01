<template>
  <div class="container" id="app">
    <Header></Header>
    <Sidebar></Sidebar>
    <router-view></router-view>
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
     
    }
  },
  methods: {
  }
}
</script>

<style lang="scss" scoped>
  @import '../static/styles/mixins.scss';

  .container {
    font-family: 'Slabo 27px', serif;
    @include displayFlex;
    @include flexWrap;
  }
</style>