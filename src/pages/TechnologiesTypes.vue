<script>
import axios from 'axios';
import { store } from '../data/store';
import Loader from '../components/Loader.vue';

export default {
    name: 'TechnologiesTypes',
    components:{
        Loader
    },
    data(){
        return{
            store,
            isLoaded: false
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
        this.getApi(store.apiUrl, 'technologies');
        this.getApi(store.apiUrl, 'types');
    }
}
</script>


<template>

    <h1 class="text-center">TechnologiesTypes</h1>

    <Loader v-if="!isLoaded" />

    <div class="container d-flex justify-content-between my-5" v-else>

        <div class="container text-center">
            <h3 class="mb-5">Technologies</h3>

            <ul>
                <li v-for="technology in store.technologies" :key="technology.id">{{ technology.name }}</li>
            </ul>

        </div>


        <div class="container text-center">
            <h3 class="mb-5">Types</h3>

            <ul>
                <li v-for="type in store.types" :key="type.id">{{ type.name }}</li>
            </ul>

        </div>

    </div>
  
</template>

<style lang="scss" scoped>

ul{
    list-style: none;
}



</style>