<script>
import { store } from '../data/store';

  export default {
    name: 'ProjectCard',
    data() {
      return {
        store
      }
    },
    computed: {},
    mounted() {},
    methods: {}
  }
</script>

<template>


<div v-for="project in store.projects" :key="project.id" class="card m-4" style="width: 18rem;">
  <div class="card-body">
    <h2 class="card-title">{{ project.name }}</h2>
    <p class="card-text">{{ project.description }}</p>
    <span><strong>Type:</strong> {{ project.type?.name }}</span>
  </div>
  <ul class="list-group list-group-flush">
    <li v-for="technology in project.technologies" :key="technology.id" class="list-group-item">{{ technology.name }}</li>
  </ul>
</div>


</template>

<style lang="scss" scoped>

</style>