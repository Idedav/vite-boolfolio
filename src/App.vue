<script>
import Header from './components/partials/Header.vue'

export default {
  name : 'App',
  components:{
      Header
    },
  data(){
    return{}
  },

  methods:{},

  mounted(){}

}
</script>

<template>
  <h1 class="text-center my-5">Boolfolio</h1>
  <Header />
    <div class="container container-custom my-5">
      <RouterView />
    </div>
</template>

<style lang="scss" scoped>
h1{
  font-weight: bold;
  font-size: 4rem;
}
</style>
