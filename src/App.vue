<script>

import axios from 'axios';
import { store } from './data/store';
import ProjectCard from './components/ProjectCard.vue';
import Loader from './components/Loader.vue';
import Navigator from './components/Navigator.vue';

export default {
  name : 'App',
  components:{
    ProjectCard,
    Loader,
    Navigator
  },
  data(){
    return{
      title: 'My Projects',
      isLoaded: false,
      links: []
    }
  },

  methods:{
    getApi(endPoint){
      this.isLoaded = false;
      axios.get(endPoint)
      .then(result =>{
        this.isLoaded = true;
        console.log(result.data.links);
        store.projects = result.data.data;
        this.links = result.data.links;
      })
    }
  },

  mounted(){
    this.getApi(store.apiUrl + 'projects');
  }

}
</script>

<template>
  <h1 class="text-center my-5">{{ title }}</h1>
  <div class="container d-flex justify-content-center align-items-center">
    <Loader v-if="!isLoaded" />
    <div class="d-flex flex-wrap justify-content-center" v-else>
      <ProjectCard />
      <Navigator :links="links" @callApi="getApi"/>
    </div>
  </div>
</template>

<style lang="scss">

</style>
