<script>

import axios from 'axios';
import { store } from './data/store';

export default {
  name : 'App',
  data(){
    return{
      title: 'Hello World'
    }
  },

  methods:{
    getApi(){
      axios.get(store.apiUrl + 'projects')
      .then(result =>{
        console.log(result.data);
      })
    }
  },

  mounted(){
    this.getApi();
  }

}
</script>

<template>
  <div class="container">
    <h1>{{ title }}</h1>
  </div>
</template>

<style lang="scss">

</style>
