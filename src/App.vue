<script>

import axios from 'axios';
import { store } from './data/store';
import ProjectCard from './components/ProjectCard.vue';

export default {
  name : 'App',
  components:{
    ProjectCard
  },
  data(){
    return{
      title: 'My Projects',
    }
  },

  methods:{
    getApi(){
      axios.get(store.apiUrl + 'projects')
      .then(result =>{
        console.log(result.data.data);
        store.projects = result.data;
      })
    }
  },

  mounted(){
    this.getApi();
  }

}
</script>

<template>
  <h1 class="text-center my-5">{{ title }}</h1>
  <div class="container d-flex flex-wrap justify-content-center">
    <ProjectCard />
  </div>
</template>

<style lang="scss">

</style>
