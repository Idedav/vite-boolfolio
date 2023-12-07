<script>

import axios from 'axios';
import { store } from '../data/store';
import ProjectCard from '../components/ProjectCard.vue';
import Loader from '../components/Loader.vue';
import { pushScopeId } from 'vue';

export default {
  name : 'ProjectDetail',
  components:{
    ProjectCard,
    Loader
  },
  data(){
    return{
      project: {},
      isLoaded: false,
    }
  },

  methods:{
    getProject(slug){
      axios.get(store.apiUrl + 'projects/get-project/' + slug)
      .then(result =>{
        if(!result.data.success){
              this.$router.push({ name: 'error-404' })
            }
        this.isLoaded = true
        this.project = result.data.project;
      })
    }
  },
  computed: {
    technologiesList(){
      return this.project.technologies?.map(technology => technology.name).join(',') || 'This Project does not have a technologies';
    }
  },

  mounted(){
    this.getProject(this.$route.params.slug);
  }

}
</script>

<template>
  <div class="container-fluid d-flex align-items-center justify-content-center flex-column">
    <h1 class="mb-5">Project Detail</h1>
    <Loader v-if="!isLoaded" />
    <div class="container" v-else>
      <h3 class="col-12 my-4"><strong>Project Name: </strong>{{ project.name }}</h3>
      <h3><strong>Description:</strong></h3>
      <p>{{ project.description }}</p>
      <h3><strong>Type:</strong></h3>
      <p>{{ project.type?.name ?? 'This Project does not have a type'}}</p>
      <h3><strong>Technologies:</strong></h3>
      <p>{{ technologiesList }}</p>

    </div>
  </div>
</template>

<style lang="scss">

</style>
