<script>

import axios from 'axios';
import { store } from '../data/store';
import ProjectCard from '../components/ProjectCard.vue';
import Loader from '../components/Loader.vue';
import Navigator from '../components/Navigator.vue';

export default {
  name : 'Projects',
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
    getApi(endPoint, type){
      this.isLoaded = false;
      axios.get(endPoint + type)
      .then(result =>{
        this.isLoaded = true;

        switch(type){
          case 'technologies':
            store.technologies = result.data;
            break;
          case 'types':
            store.types = result.data;
            break;
          default:
            store.projects = result.data.data;
            this.links = result.data.links;
        }
      })
    }
  },

  mounted(){
    this.getApi(store.apiUrl, 'projects');
  }

}
</script>

<template>
  <div class="container-fluid d-flex align-items-center justify-content-center flex-column">
    <h1 class="text-center col-12 mb-4">{{ title }}</h1>
    <Loader v-if="!isLoaded" />
    <div v-else>
      <div class="d-flex flex-wrap justify-content-center">
        <ProjectCard />
        <Navigator :links="links" @callApi="getApi"/>
      </div>
    </div>
  </div>
</template>

<style lang="scss">

</style>
