<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab">
      <div class="tab-item">
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller">商家</router-link>
      </div>
    </div>
    <router-view></router-view>
  </div>
</template>

<script type="text/ecmascript-6">
  import header from './components/header/header.vue';
  const ERR_OK = 0;

  export default {
    name: 'App',
    data() {
      return {
        seller: {}
      };
    },
    created(){
      this.$http.get('/api/seller').then(response => {
        // success callback
        response = response.body;
        if (response.errno === ERR_OK) {
          this.seller = response.data;
          console.warn(this.seller);
        }
      }, response => {
        // error callback
      });
    },
    components: {
      'v-header': header
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  #app
    .tab
      display: flex
      width: 100%
      height: 40px
      line-height: 40px
      .tab-item
        flex: 1
        text-align: center
</style>
